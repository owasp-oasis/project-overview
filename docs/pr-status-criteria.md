# OASIS PR Status Criteria

**Version:** 1.0  
**Last Updated:** June 24, 2026

## Overview

Each pull request in the OASIS fork receives a status classification that reflects its lifecycle and community consensus. This document defines all five statuses, their classification conditions, priority ranking, and visual representation.

## Status Definitions

### 1. Accepted (Highest Priority)

**Badge Color:** Purple (`#ede9fe` background, `#5b21b6` text)

**Definition:** The security fix was merged into the upstream repository and the fork PR is now closed.

**Classification Conditions:**
- PR state: `closed`
- `merged_upstream = 1` (confirmed via GitHub API SHA lookup in upstream repo)

**Meaning:** The fix has been officially adopted upstream. This represents the most successful outcome for OASIS work.

**How It Works:**
The sync engine checks whether the PR's head commit SHA exists in the upstream repository via `GET /repos/{upstream}/commits/{sha}`. If found (HTTP 200), `merged_upstream` is set to 1.

---

### 2. Trusted

**Badge Color:** Green (`#dcfce7` background, `#166534` text)

**Definition:** Open PR that meets the trust threshold for community consensus. Ready to be considered for upstream submission.

**Classification Conditions:**
- PR state: `open`
- `participants >= 10` (distinct users who cast OASIS-template votes)
- `consensus_accept / total_votes >= 0.75` (75%+ of votes are Accept)

**Meaning:** The PR has strong community support and enough engagement to indicate its quality. It is a prime candidate for upstream submission.

**Thresholds:** 
- Minimum contributors: 10
- Minimum accept rate: 75%

**Status:** These thresholds are a stub pending community ratification.

---

### 3. Needs Review

**Badge Color:** Yellow (`#fef9c3` background, `#854d0e` text)

**Definition:** Open PR in the OASIS fork that has not yet reached the minimum criteria for an OASIS Stamp of Trust.

**Classification Conditions:**
- PR state: `open`
- Does not meet Trusted criteria (insufficient participants or accept rate below 75%)

**Meaning:** The PR is still under community review and awaiting more engagement or clarification. Validators are encouraged to review and vote.

---

### 4. Withdrawn

**Badge Color:** Orange (`#ffedd5` background, `#9a3412` text)

**Definition:** The OASIS community voted to accept this finding. The fork PR was closed without a confirmed upstream merge — the fix may have landed via a separate PR or commit.

**Classification Conditions:**
- PR state: `closed`
- `merged_upstream = 0` (upstream merge not detected via SHA lookup)
- `consensus_accept > 0` (at least one OASIS accept vote recorded)

**Meaning:** The community clearly supported this fix (with accept votes), but the PR in the fork was closed without the exact head SHA appearing in the upstream repo. This can happen when:
- The upstream maintainer merged the fix via a different PR
- The upstream maintainer squash-merged the commits (creating a new SHA)
- The upstream maintainer rebased the commits
- The upstream maintainer cherry-picked the changes

The Withdrawn status signals that OASIS workers engaged meaningfully with this vulnerability and reached consensus, even though we cannot confirm the exact commit SHA in the upstream.

**Priority Note:** Withdrawn takes priority over Rejected. Even if there are also reject votes, any accept vote triggers Withdrawn status.

---

### 5. Rejected (Lowest Priority)

**Badge Color:** Red (`#fee2e2` background, `#991b1b` text)

**Definition:** The fork PR was closed with no accept votes recorded. The fix was not adopted.

**Classification Conditions:**
- PR state: `closed`
- `merged_upstream = 0` (upstream merge not detected)
- `consensus_accept = 0` (no OASIS accept votes)

**Meaning:** The PR was closed without clear community acceptance. This can indicate:
- The issue was deemed out-of-scope or invalid
- The PR was withdrawn by the author
- The community voted against the fix (reject votes present)
- No OASIS community engagement occurred

---

## Priority Ranking

The statuses are ranked by the value and trust they signal:

```
Accepted > Trusted > Needs Review > Withdrawn > Rejected
```

| Rank | Status | Type | Signal |
|---|---|---|---|
| 1 | Accepted | Closed | Upstream merge confirmed |
| 2 | Trusted | Open | Strong community consensus |
| 3 | Needs Review | Open | Under active review |
| 4 | Withdrawn | Closed | Community accepted, upstream unclear |
| 5 | Rejected | Closed | No community acceptance |

This ranking reflects both the outcome achieved and the level of trust/engagement demonstrated by OASIS workers.

---

## Classification Logic (Pseudocode)

```
if (pr.state === 'closed') {
  if (pr.merged_upstream === 1) {
    return 'Accepted'
  } else if (pr.consensus_accept > 0) {
    return 'Withdrawn'
  } else {
    return 'Rejected'
  }
}

if (pr.state === 'open') {
  const totalVotes = pr.consensus_accept + pr.consensus_modify + pr.consensus_reject
  const acceptRate = totalVotes > 0 ? pr.consensus_accept / totalVotes : 0
  
  if (pr.participants >= 10 && acceptRate >= 0.75) {
    return 'Trusted'
  } else {
    return 'Needs Review'
  }
}
```

---

## Data Sources

All status determinations are computed entirely from the `pull_requests` table:
- `state` — from GitHub API (open/closed)
- `merged_upstream` — computed via upstream SHA lookup
- `consensus_accept`, `consensus_modify`, `consensus_reject` — aggregated from `pr_comments` table via `parseDecision()` function
- `participants` — count of distinct users with ≥1 OASIS-template vote

**Note:** Status is a frontend-computed value, not stored in the database. It is calculated on every page load based on current DB values.

---

## Known Limitations & Future Improvements

### Limitation 1: Upstream Merge Detection (Option 3 TODO)
Current SHA lookup via `GET /repos/{upstream}/commits/{sha}` fails when:
- The upstream maintainer squash-merged (new SHA)
- The upstream maintainer rebased commits
- The upstream maintainer cherry-picked changes
- The PR was closed but the fix landed in a different PR

**Future Improvement:** Implement squash/rebase/cherry-pick-aware upstream detection by:
1. Checking GitHub PR merge status (`GET /pulls/{n}/merge`)
2. Searching upstream commit tree by content hash (not SHA)
3. Cross-referencing by commit message patterns

### Limitation 2: PR Author vs. Maintainer Closure
The current logic does not distinguish between:
- An author self-closing their PR (withdrawal)
- A maintainer closing a PR (acceptance or rejection)

**Future Improvement:** Fetch GitHub Issues Events API (`GET /issues/{n}/events`) to capture the `closed_by` actor. Use this signal to refine Withdrawn classification.

### Limitation 3: "Accepted" Manual Detection
The initial implementation of upstream merge detection was marked as TODO. This has been addressed with automatic SHA lookup, but complex merge strategies (squash, rebase, cherry-pick) are not yet handled. See Limitation 1.

---

## Implementation Notes

**File:** `src/pages/leaderboards/PRsTab.tsx:67–75` — `getOASISStatus()` function

**Sync Engine:** `worker/sync.ts:210–221` — computes `merged_upstream` flag

**OASIS Vote Parsing:** `worker/github.ts:118–135` — `parseDecision()` extracts votes from OASIS-template comments

**UI Rendering:** `src/pages/leaderboards/PRsTab.tsx:86–108` — `STATUS_DEFINITIONS` array and `StatusKey` component

---

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2026-06-24 | Initial specification. Added Withdrawn status (previously all closed non-merged PRs were Rejected). Defined priority ranking. |

