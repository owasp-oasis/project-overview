# OASIS Trust Score Criteria

**Version:** 1.0  
**Status:** Specification  
**Last Updated:** June 15, 2026

---

## Table of Contents

1. [Overview](#overview)
2. [Core Formula](#core-formula)
3. [Component Definitions](#component-definitions)
4. [Bonus Factors](#bonus-factors)
5. [90-Day Ranking](#90-day-ranking)
6. [Database Schema](#database-schema)
7. [Computation & Updates](#computation--updates)
8. [Examples](#examples)

---

## Overview

The OASIS Trust Score measures validator credibility and contribution quality within the OASIS program. It combines raw contribution metrics with time-sensitive and influence bonuses to reward thoughtful participation and consistent engagement.

**Key Goals:**

- Recognize validators who provide accurate, timely feedback on security vulnerabilities
- Encourage participation in underrepresented vulnerability classes (CWEs)
- Surface emerging and consistent contributors
- Provide transparency into how reputation is earned
- Enable skill-based matching of validators to tasks

---

## Core Formula

### Base Reputation

```
base_reputation = comment_score + peer_score + reaction_score + trust_score
```

### Modified Reputation

```
modified_reputation = base_reputation × (1 + early_mover + early_bird + influencer)
```

### Final Score

The `modified_reputation` is the primary display value for leaderboards and validator panels. The `rank_90d` is computed as a secondary metric restricted to activity in the last 90 days, refreshed during each sync cron job.

---

## Component Definitions

### comment_score

**Formula:**  
```
comment_score = count(OASIS-template comments posted)
```

**Definition:** Number of times the validator has posted a complete OASIS-template comment. Each comment counts as 1 point, regardless of decision (accept/modify/reject/duplicate).

**Why:** Encourages participation by rewarding any substantive engagement.

**Range:** 0 to N (unbounded)

---

### peer_score

**Formula:**  
```
peer_score = Σ(peer_agreement_per_reaction)
```

Where each reaction received on a validator's OASIS comment contributes:

- **+0.25** (base) if the reaction is present
- **+0.10** (positive adjustment) for reactions that indicate agreement (👍 +1)
- **−0.50** (negative adjustment) for reactions that indicate disagreement (👎 −1)

**Aggregation:** Sum across all reactions received on all OASIS comments by this validator.

**Why:** Peer agreement is a strong signal of comment quality and accuracy. Negative reactions indicate potential disagreement with the validator's analysis.

**Example:**
- 10 +1 reactions: `10 × (0.25 + 0.10) = 3.5`
- 2 -1 reactions: `2 × (0.25 - 0.50) = -0.50`
- Total peer_score: `3.5 - 0.50 = 3.0`

**Range:** Unbounded (can be negative if validator receives many -1 reactions)

---

### reaction_score

**Formula:**  
```
reaction_score = min(reactions_given, 5) × 0.25
```

**Definition:** The number of reactions the validator has given to *other validators'* OASIS comments, capped at 5. Each contribution to the discussion is weighted at 0.25 points.

**Why:** Recognizes validators who engage with peers' analysis and contribute to consensus-building. Capped at 5 to avoid reward inflation.

**Range:** 0 to 1.25 (max when ≥5 reactions given; self-reactions excluded)

---

### trust_score

**Formula:**  
```
trust_score = 10 × count(PRs voted accept AND merged upstream)
```

**Definition:** High weight (10 points each) for PRs where the validator voted "accept" and the PR was successfully merged into the upstream project.

**Why:** Validates the accuracy of the validator's assessment. Accepting a PR that merges proves the fix was good; rejecting a PR that later merges would lower confidence.

**Range:** 0 to 10N (where N = number of accepted + merged PRs)

---

## Bonus Factors

Bonuses are applied multiplicatively: `1 + (sum of applicable bonuses)`.

### early_mover

**Formula:**  
```
early_mover = 
  + 0.20 if validator is in first 1% of commenters on a PR (after 72h from creation)
  + 0.10 if validator is in 1–10% (after 72h)
  + 0.05 if validator is in 10–25% (after 72h)
```

**Definition:** Rewards validators who post analysis early in a PR's lifecycle. The "after 72h" clause prevents immediate comments from receiving outsized weight; the bonus applies to comments posted after the PR has been visible for 3 days.

**Why:** Early analysis sets the tone for the review cycle and demonstrates proactive engagement.

**Range:** 0 to +0.20 per PR (applied once, max +0.20 per PR × modifier across all PRs)

---

### early_bird

**Formula:**  
```
early_bird =
  + 0.25 if validator commented ≤24 hours after PR creation
  + 0.10 if validator commented ≤96 hours (4 days) after PR creation
```

**Definition:** Rewards rapid response. A validator earns +0.25 for responding within 24h, or +0.10 if they respond within 96h but after 24h.

**Why:** Demonstrates attentiveness and reduces PR queue time.

**Range:** 0, +0.10, or +0.25 per PR (applied once per PR)

---

### influencer

**Formula:**  
```
influencer =
  + 0.10 if validator has the most total reactions across all comments on a PR
  + 0.20 if validator has the most positive (+1) reactions across all comments on a PR
  − 0.50 if validator has the most negative (−1) reactions across all comments on a PR
```

**Definition:** Recognizes whose analysis resonates with peers (positive) or creates friction (negative). Applied per PR.

**Why:** Identifies thought leaders whose analysis influences consensus, and flags potential polarizing commenters.

**Range:** −0.50 to +0.20 per PR

---

## 90-Day Ranking

### rank_90d

**Formula:**  
```
rank_90d_reputation = base_reputation restricted to comments posted in last 90 days
rank_90d = ordinal position when all contributors are sorted DESC by rank_90d_reputation
```

**Definition:** A secondary ranking that captures recent momentum. Computed by rerunning the full reputation formula using only comments posted in the last 90 days, then ranking contributors in descending order.

**Why:** Highlights recently active validators and helps surface new talent. Used in the leaderboard's "Recent Activity" view.

**When Updated:** Each sync cron job recomputes this ranking.

**Range:** 1 to N (position in leaderboard)

---

## Database Schema

The contributor reputation data is stored in the `contributors` table:

```sql
CREATE TABLE contributors (
  login                  TEXT PRIMARY KEY,
  avatar_url             TEXT,
  
  -- Activity metrics
  prs_worked             INTEGER DEFAULT 0,
  total_interactions     INTEGER DEFAULT 0,
  non_oasis_interactions INTEGER DEFAULT 0,  -- tracked but not used in reputation
  reactions_received     INTEGER DEFAULT 0,
  reactions_given        INTEGER DEFAULT 0,
  accepts                INTEGER DEFAULT 0,
  modifies               INTEGER DEFAULT 0,
  rejects                INTEGER DEFAULT 0,
  duplicates             INTEGER DEFAULT 0,
  
  -- Reputation score components (pre-computed)
  comment_score          REAL DEFAULT 0,
  peer_score             REAL DEFAULT 0,
  reaction_score         REAL DEFAULT 0,
  trust_score            REAL DEFAULT 0,
  
  -- Final scores
  base_reputation        REAL DEFAULT 0,
  modified_reputation    REAL DEFAULT 0,
  
  -- 90-day metrics
  rank_90d               INTEGER,
  rank_90d_oldest_activity TEXT,  -- ISO-8601
  
  synced_at              TEXT
);
```

Supporting tables:

```sql
-- Per-comment granular data for bonus factor computation
CREATE TABLE pr_comments (
  id             INTEGER PRIMARY KEY,
  pr_id          INTEGER NOT NULL,
  repo_name      TEXT NOT NULL,
  pr_number      INTEGER NOT NULL,
  login          TEXT NOT NULL,
  decision       TEXT,  -- 'accept'|'modify'|'reject'|'duplicate'|NULL
  duplicate_of   INTEGER DEFAULT NULL,
  created_at     TEXT NOT NULL,  -- ISO-8601
  pr_created_at  TEXT NOT NULL   -- ISO-8601
);

-- Per-reaction data for peer_score aggregation
CREATE TABLE comment_reactions (
  id              INTEGER PRIMARY KEY,
  comment_id      INTEGER NOT NULL,
  reactor_login   TEXT NOT NULL,
  reaction_type   TEXT NOT NULL,  -- '+1'|'-1'|'heart'|'laugh'|...
  created_at      TEXT NOT NULL
);
```

---

## Computation & Updates

### Initial Build (rebuildContributors)

When the sync pipeline runs, it:

1. **Aggregates raw metrics** from `pr_comments` and `comment_reactions` tables
2. **Computes component scores:**
   - `comment_score`: COUNT of rows in `pr_comments` per login
   - `peer_score`: SUM of peer agreement factors from `comment_reactions`
   - `reaction_score`: MIN(reactions_given, 5) × 0.25
   - `trust_score`: COUNT(accept comments where PR merged upstream) × 10

3. **Computes bonus factors** (per PR):
   - Early_mover: rank within 72h comment window
   - Early_bird: comment time relative to PR creation
   - Influencer: reaction count leadership

4. **Applies bonuses:**
   - `base_reputation = comment_score + peer_score + reaction_score + trust_score`
   - `modified_reputation = base_reputation × (1 + Σ bonuses)`

5. **Computes 90-day rank:** Re-run steps 1–4 using only comments from the last 90 days

6. **Writes results** back to the `contributors` table

### Update Frequency

- **Full recompute:** Each sync cron job (currently daily or on-demand)
- **Incremental updates:** New comments and reactions are added to the per-comment tables immediately; reputation is recomputed at the next cron run

---

## Examples

### Example 1: Baseline Contributor

**Raw Data:**
- Posted 5 OASIS comments
- Received 8 +1 reactions, 1 -1 reaction
- Gave 2 reactions to other comments
- 2 PRs voted accept and merged upstream
- Posted 1st comment 30h after PR creation

**Calculation:**

```
comment_score    = 5
peer_score       = (8 × 0.35) + (1 × (-0.25)) = 2.80 - 0.25 = 2.55
reaction_score   = min(2, 5) × 0.25 = 0.50
trust_score      = 2 × 10 = 20.00

base_reputation  = 5 + 2.55 + 0.50 + 20 = 28.05

Bonuses (example):
early_bird       = +0.10 (posted 30h after creation, so ≤96h but >24h)
early_mover      = +0.05 (assume 2nd-quartile commenter)
influencer       = +0.10 (assume tied for most total reactions on one PR)
total_bonus      = 0.25

modified_reputation = 28.05 × (1 + 0.25) = 28.05 × 1.25 = 35.06
```

---

### Example 2: High-Friction Contributor

**Raw Data:**
- Posted 10 OASIS comments
- Received 3 +1 reactions, 8 -1 reactions
- Gave 1 reaction
- 3 PRs voted accept and merged upstream
- Always posts early

**Calculation:**

```
comment_score    = 10
peer_score       = (3 × 0.35) + (8 × (-0.25)) = 1.05 - 2.00 = -0.95
reaction_score   = min(1, 5) × 0.25 = 0.25
trust_score      = 3 × 10 = 30.00

base_reputation  = 10 + (-0.95) + 0.25 + 30 = 39.30

Bonuses (example):
early_bird       = +0.25 (consistently ≤24h)
early_mover      = +0.10 (top 10%)
influencer       = -0.50 (most -1 reactions on latest PR)
total_bonus      = -0.15

modified_reputation = 39.30 × (1 + (-0.15)) = 39.30 × 0.85 = 33.41
```

Despite high comment and accept counts, negative peer feedback reduces the final score.

---

## Design Rationale

### Why Peer Score Over Accuracy Direct Measurement?

We cannot directly measure whether a validator's analysis was correct (a PR might be merged for political or deadline reasons). Peer agreement via reactions is a proxy: validators who post widely-agreed-upon analysis receive positive peer_score.

### Why Cap Reactions Given?

Reactions are a secondary contribution. Capping at 5 reactions (1.25 points max) ensures validators can't game the system by spamming reactions. It's a fringe benefit, not a primary path to reputation.

### Why Trust Score Weight at 10×?

An accept vote that results in an upstream merge is strong evidence the validator was correct. Weighting it 10× (vs. 1× for comments) reflects the high confidence in this signal. It's also significant enough to make a material difference in the final score.

### Why 90-Day Ranking?

Long-term contributors should dominate the all-time rankings. The 90-day view surfaces emerging talent and recent activity spikes, encouraging sustained engagement.

### Why Multiply by (1 + bonuses)?

Additive bonuses would cap out and lose impact. Multiplicative growth scales with the validator's base reputation: a high-performing validator with early-bird behavior gains more than a low-performing validator with the same behavior.

---

## Future Enhancements

- **CWE-Scoped Reputation:** Track reputation separately per CWE class to identify specialists
- **Language-Specific Expertise:** Reputation adjusted by programming language (Go, JavaScript, Python, etc.)
- **Decay Over Time:** Apply a time-decay factor to older contributions
- **Community Voting:** Allow other validators to flag unhelpful or misleading comments
- **Weighted Credibility Ledger:** More granular trust scoring for high-stakes decisions (e.g., accepting critical CVEs)

---

## Version History

| Version | Date       | Changes |
|---------|------------|---------|
| 1.0     | 2026-06-15 | Initial specification published |

