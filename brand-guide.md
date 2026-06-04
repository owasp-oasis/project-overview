# OASIS Brand Guide

**OASIS — Open Automated Security Initiative for Software**

This guide is the authoritative reference for how OASIS is named, described, written about, and visually represented. It is for contributors, volunteers, community members, and anyone producing content on behalf of OASIS.

---

## Contents

1. [Overview](#1-overview)
2. [Name & Usage](#2-name--usage)
3. [Terminology Glossary](#3-terminology-glossary)
4. [Voice & Tone](#4-voice--tone)
5. [Key Messages](#5-key-messages)
6. [Guiding Principles](#6-guiding-principles)
7. [Color Palette](#7-color-palette)
8. [Typography](#8-typography)
9. [Logo & Lockup](#9-logo--lockup)
10. [UI Patterns](#10-ui-patterns)
11. [Writing Style](#11-writing-style)

---

## 1. Overview

OASIS — Open Automated Security Initiative for Software — is a community-driven project that mobilizes the AppSec community to deliver human-validated vulnerability fixes for the open source software that runs the world.

Fix automation tools can now generate candidate security patches at the speed of compute. What they cannot do is make those patches credible to the open source maintainers who must decide whether to merge them. OASIS is the community validation layer between fix automation and upstream maintainers. AppSec professionals review candidate fixes, separate real signal from AI-generated noise, and help trustworthy fixes reach the projects that need them.

The brand rests on three qualities:

- **Urgency** — AI threats are exploiting open source faster than any one team can respond
- **Credibility** — community validation, not automation, is what makes a fix trustworthy
- **Community** — this work belongs to practitioners, not vendors

---

## 2. Name & Usage

### Brand name

The project name is **OASIS**. Always write it in all-caps.

- Correct: **OASIS**
- Incorrect: Oasis, oasis, O.A.S.I.S.

### Long-form name

On first mention in formal documents, press materials, or any context where the audience may not know what OASIS stands for, write:

> **OASIS (Open Automated Security Initiative for Software)**

After the first mention, use **OASIS** alone.

### OWASP relationship

OASIS has submitted a project proposal to OWASP and is currently seeking formal approval. Until that approval is granted:

- **Do not** use "OWASP OASIS" as the brand name
- **Do not** describe OASIS as an OWASP project
- **Do** say: *"OASIS has submitted a project proposal to OWASP."*
- **Do** say: *"OASIS is pursuing OWASP project status."*

The homepage currently displays a status kicker reading "Proposed OWASP project — open now." This is a factual status disclosure, not a brand-level claim. It will be updated when project status changes. Do not replicate this phrasing in new materials.

### "Team OASIS"

"Team OASIS" is an accepted informal variant used to refer to the community of validators, contributors, and project owners working within the OASIS model. It is appropriate in outreach, registration calls, and community-facing copy.

- Acceptable: *"Join Team OASIS"*
- Not appropriate in formal documents, press releases, or technical documentation

---

## 3. Terminology Glossary

OASIS uses precise, consistent terminology throughout all documentation and community communication. Using the wrong term — even a synonym — undermines the credibility of the project.

### Canonical terms

| Use this | Not this | Why |
|---|---|---|
| **candidate fix** | AI fix, patch, PR, submission | Neutral. Does not presuppose quality or correctness. |
| **validator** | reviewer, approver, auditor | The specific OASIS role. "Reviewer" is too generic. |
| **fix automation** | AI, AI tools, LLM | Broader and more accurate. The tools include SAST, dependency analysis, and LLM-assisted generation. |
| **project owner** | admin, lead, maintainer | The OASIS governance role. "Maintainer" always refers to upstream OSS maintainers. |
| **maintainer** | (context-specific) | Always refers to upstream open source project maintainers — never OASIS project leads. |
| **upstream submission** | going live, shipping, merging | Precise. The fix is *offered*, not automatically merged. |
| **upstream acceptance** | approval, merge, success | Maintainers decide. Acceptance is their action. |
| **validation** | review, approval, sign-off | The OASIS-specific process of structured human assessment. |
| **credibility-weighted** | democratic, voted, rated | The scoring model weighs expertise, not just volume. |

### Terms to avoid

- **AI slop PRs** — acceptable in informal community discussion and blog posts where the problem is being described; not appropriate in formal project documentation or press materials
- **bug fix** — OASIS works on vulnerability fixes, not general bugs
- **scan** — too narrow; OASIS uses multiple tools including SAST, dependency analysis, and LLM-assisted generation
- **approve** — maintainers *accept* upstream PRs; OASIS project owners *adopt* candidate fixes

---

## 4. Voice & Tone

OASIS communicates with directness, technical credibility, and a sense of shared urgency. The audience is AppSec practitioners — they can read code, they have opinions, and they respect precision over polish.

### Brand personality

| Trait | What it sounds like |
|---|---|
| **Direct** | Short sentences. Active voice. No throat-clearing. |
| **Urgent** | The problem is real and the window to act is now. This comes through in the writing, not in exclamation marks. |
| **Technically credible** | We name things correctly. We don't oversimplify or overclaim. |
| **Community-first** | This work belongs to practitioners. Vendors are contributors, not authorities. |
| **Unpretentious** | No buzzwords. No jargon for its own sake. If a simpler word works, use it. |

### Tone by context

| Context | Tone |
|---|---|
| Homepage / outreach | Energized, inclusive, action-oriented |
| Technical documentation | Precise, neutral, operational |
| GitHub issues / PRs | Functional. State what happened, what's needed, what was decided. |
| Press / media | Measured. Let the work speak. Avoid superlatives. |
| Community onboarding | Welcoming, practical, low-barrier |

### Do

- Use "you" and "we" — this is a community
- Use concrete numbers and real examples when available
- Name the problem plainly: "AI tools are flooding repositories with unvetted fix proposals"
- Be specific about what the work actually involves: "A single validation takes roughly eight minutes"

### Don't

- Use phrases like "revolutionary," "cutting-edge," "world-class," or "game-changing"
- Claim more than the data supports
- Write in the passive voice habitually
- Use scare quotes around "AI" or "automation" — treat them as the tools they are

---

## 5. Key Messages

These are the canonical phrasings for OASIS's most important messages. Use them exactly or use them as the baseline when adapting for context.

### Primary tagline

> Open source powers the world. Vibe hacking exploits it. Team OASIS fixes it.

This three-part structure is intentional. It states the stakes, names the threat, and introduces the community. Do not abbreviate to just the third line.

### Mission statement

> OASIS mobilizes the AppSec community to deliver community-validated vulnerability fixes for the open source software that runs the world.

### Short descriptor

> OASIS is the community validation layer between fix automation and upstream maintainers.

Use this when introducing OASIS in a sentence — in bios, speaker introductions, sponsor decks, or PR body text.

### Footer descriptor

> Vendor-neutral. Community-driven. Open source.

Three short phrases that anchor the brand's ethical position. Use them together.

### CTA line

> Take 5 minutes. Help secure the software that runs the world.

For registration calls, event outreach, and community sign-up prompts.

### Problem statement

> Open-source maintainers are drowning in noise. AI tools are flooding repositories with unvetted fix proposals. Maintainers push back on all AI-generated contributions, even the good ones. Real vulnerabilities go unfixed.

### Solution statement

> Tens of thousands of AppSec professionals have exactly the expertise needed to validate those fixes — and no mechanism to deliver it. OASIS provides that mechanism.

---

## 6. Guiding Principles

Three principles govern everything OASIS does — how repositories are selected, how fixes are validated, and how the community works together. They may be referenced by single-word tags: **Impact**, **Credibility**, **Village**.

### Impact

*Focus on impact.*

Work on repositories where upstream acceptance is plausible. Measure success by acceptance rate, not activity volume.

**OASIS will:**
- Work on repositories where upstream acceptance is plausible
- Minimize implementation effort
- Measure success by upstream acceptance rate, not activity metrics

**OASIS will not:**
- Aim for raw PR volume
- Wait for opt-in from upstream projects before beginning

### Credibility

*Acceptance builds credibility.*

Treat automation as a source of candidate fixes, not a source of truth. Human review is what makes a fix trustworthy.

**OASIS will:**
- Treat automation as a source of candidate fixes, not a source of truth
- Require human validation before any upstream submission
- Use weighted reviewer credibility rather than a fixed approval count
- Clearly communicate OASIS community review in every upstream PR

**OASIS will not:**
- Submit AI-generated fixes directly to upstream projects without human review
- Claim to bypass maintainers — maintainers still decide what merges

### Village

*It takes a village.*

Keep the authoritative review and decision process under the OASIS project. This work belongs to the community.

**OASIS will:**
- Keep the authoritative review and decision process transparent and community-owned
- Operate on GitHub so the workflow is auditable by anyone
- Build trusted relationships between validators, project owners, and maintainers
- Welcome validators at all experience levels

**OASIS will not:**
- Allow any single vendor to control governance, fix selection, or validation outcomes
- Publicly expose unresolved vulnerabilities by default

---

## 7. Color Palette

All colors are defined as CSS custom properties in `src/index.css` of the website project. Use the hex values when working outside the web codebase (presentations, documents, design tools).

### Primary palette

| Name | Hex | CSS Token | Role |
|---|---|---|---|
| Ink | `#07111f` | `--ink` | Primary text, headings on light backgrounds |
| Ink Soft | `#243247` | `--ink-soft` | Secondary text, subheadings |
| Muted | `#61738b` | `--muted` | Tertiary text, captions, placeholders |
| Blue Dark (Navy) | `#0b4f8a` | `--blue-dark` | Primary brand navy; shield outer layer; dark section backgrounds |
| Blue | `#0f6fcf` | `--blue` | Primary interactive blue; links; secondary buttons; inner shield |
| Blue Mid | `#1558d6` | `--blue-mid` | Italic/emphasis text in hero headlines |
| Blue Soft | `#e7f1ff` | `--blue-soft` | Blue tint backgrounds; hover states; badge backgrounds |
| Green | `#0d9e52` | `--green` | Success states; the "fixes it" headline line; green text labels |
| Green Bright | `#4cd964` | `--green-bright` | Primary CTA button background; circuit node accent on the logo icon |
| Green Soft | `#e8f9ef` | `--green-soft` | Green tint backgrounds; green badge backgrounds |
| Paper | `#f7fbff` | `--paper` | Page background; the default canvas |
| White | `#ffffff` | `--white` | Card backgrounds; text on dark surfaces |

### Gray scale

| Name | Hex | CSS Token | Role |
|---|---|---|---|
| Gray 100 | `#f4f7fb` | `--gray-100` | Subtle backgrounds |
| Gray 200 | `#e8edf5` | `--gray-200` | Borders, dividers on neutral surfaces |
| Gray 400 | `#9aacbe` | `--gray-400` | Disabled states, placeholder icons |
| Gray 600 | `#4a5c70` | `--gray-600` | Secondary text on light gray backgrounds |
| Gray 800 | `#1e2d3d` | `--gray-800` | Near-black for dense UI contexts |

### Border and shadow

| Name | Value | CSS Token | Role |
|---|---|---|---|
| Line | `rgba(15, 111, 207, .16)` | `--line` | Default borders; blue-tinted dividers |
| Line Strong | `rgba(15, 111, 207, .28)` | `--line-strong` | Emphasized borders |
| Shadow | `0 18px 50px rgba(11, 79, 138, .14)` | `--shadow` | Card elevation |

### Color usage rules

- **Navy (`#0b4f8a`)** is the dominant brand color. Use it for the logo shield, dark section backgrounds, and registration card gradients. Do not use it for body text on light backgrounds — it lacks sufficient contrast at small sizes.
- **Blue (`#0f6fcf`)** is the interactive color. Links, buttons, and active states.
- **Green Bright (`#4cd964`)** is the accent. Use it sparingly — primary CTA buttons, the logo circuit nodes, status indicators. Do not use it as a background for large text blocks.
- **Paper (`#f7fbff`)** is the page background. Do not replace it with pure white (`#ffffff`) for page backgrounds — the slight blue warmth is intentional.
- **Ink (`#07111f`)** is the primary text color. Do not use pure black (`#000000`).

### Contrast

| Combination | Ratio | WCAG |
|---|---|---|
| Ink `#07111f` on Paper `#f7fbff` | ~17:1 | AAA |
| Blue `#0f6fcf` on White | ~4.6:1 | AA |
| Green Bright `#4cd964` on Blue Dark `#0b4f8a` | ~5.8:1 | AA (large text) |
| White on Blue `#0f6fcf` | ~4.6:1 | AA |
| White on Navy `#0b4f8a` | ~8.5:1 | AAA |

Do not use Green Bright as a text color on light backgrounds — it fails AA at body text sizes.

---

## 8. Typography

OASIS uses three typefaces, each with a specific role. Do not substitute.

### Typefaces

| Typeface | CSS Token | Role | Fallbacks |
|---|---|---|---|
| **DM Serif Display** | `--serif` | Hero headlines, large display text | Georgia, serif |
| **Geist** | `--sans` | Body text, UI copy, navigation, buttons | system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif |
| **Geist Mono** | `--mono` | Eyebrows, labels, badges, kicker pills, code, step numbers | "Courier New", monospace |

### Type hierarchy

| Level | Typeface | Size | Weight | Use |
|---|---|---|---|---|
| Hero headline | DM Serif Display | `clamp(38px, 4vw, 48px)` | 400 | Homepage H1 only |
| Display H2 | DM Serif Display | `clamp(34px, 4.3vw, 56px)` | 400 | Section headings in marketing sections |
| Page H1 | Geist | `clamp(2rem, 5vw, 3rem)` | Bold | Inner page heroes |
| Body large | Geist | 18–21px | 400 | Hero lede, intro paragraphs |
| Body | Geist | 16px | 400 | Default body copy; line-height 1.7 |
| Body small | Geist | 14–15px | 400 | Card body, secondary descriptions |
| Label / eyebrow | Geist Mono | 12px | 600–700 | ALL CAPS, letter-spacing 0.08–0.14em |
| Button | Geist | 16px (1rem) | 700 | |
| Badge | Geist Mono | 0.78rem | 600 | ALL CAPS, letter-spacing 0.04em |

### Usage rules

- **DM Serif Display** is used only for hero and large display headings. It is not appropriate for body copy, buttons, labels, or UI elements.
- **Geist Mono** carries OASIS's technical voice. Use it for eyebrows ("The mechanism"), section kickers, badge text, step numbers, and any label that functions as a structured tag rather than prose.
- **Line-height:** headings `1.2`, body paragraphs `1.7`, lede text `1.55`.
- **Font smoothing:** `antialiased` is set globally. Do not override.

---

## 9. Logo & Lockup

### Logo anatomy

The OASIS logo is a shield that doubles as the letter "O" in OASIS. The wordmark reads as "OASIS" with the shield icon serving as the O, followed by "ASIS" in text.

**Shield layers:**
- **Outer shield** — Navy `#0b4f8a`. The protective container. Represents the security mission.
- **Inner shield** — Blue `#0f6fcf`. Represents the OASIS process layer between automation and upstream.
- **White donut ring** — The letter O. The central void that makes the shield readable as the first letter of OASIS.
- **Three green circuit nodes** — Green Bright `#4cd964`. Three lines extending from the ring to terminal dots, radiating from the left, top, and right positions. These represent the three validator signals in the community review process.

The circuit nodes are the only element of the logo that uses the accent green. Do not remove them or alter their color.

### Logo variants

Three variants are available. All are provided as SVG and PNG.

#### 1. Icon only — `oasis-logo`

The shield icon alone, without any text. A 256×256 square composition.

**Use for:**
- Browser favicons
- App icons and touch icons
- Social media profile pictures
- Avatar placeholders
- Contexts where the text "OASIS" is already present nearby and the icon serves as a visual anchor

**Files:**
- `project-overview/logo/svg/oasis-logo.svg`
- `project-overview/logo/png/oasis-logo.png`
- `owasp-oasis-app/public/logo/oasis-logo.svg`

---

#### 2. Wordmark — `oasis-wordmark`

The shield icon used as the "O," followed by "ASIS" in bold sans-serif text. A 640×256 (5:2 ratio) composition.

**Use for:**
- Navigation bar / site header (primary use)
- Email signatures
- Slide headers
- Any context where the logo needs to identify the project in a horizontal layout

**Files:**
- `project-overview/logo/svg/oasis-wordmark.svg`
- `project-overview/logo/png/oasis-wordmark.png`
- `owasp-oasis-app/public/logo/oasis-wordmark.svg`

---

#### 3. Full wordmark — `oasis-wordmark-full`

The wordmark with the long-form name "Open Automated Security Initiative for Software" as a two-line subtitle beneath the OASIS text. A 640×256 composition.

**Use for:**
- Formal documents (proposals, reports, grant applications)
- Conference presentations where the acronym may not be known
- Press materials and media kits
- First-page / cover-page uses

**Files:**
- `project-overview/logo/svg/oasis-wordmark-full.svg`
- `project-overview/logo/png/oasis-wordmark-full.png`
- `owasp-oasis-app/public/logo/oasis-wordmark-full.svg`

---

### Clear space

The minimum clear space around any logo variant is **1× the height of the shield icon** on all four sides.

For the icon (256px canvas), this is approximately 26px at native size. Scale proportionally for other sizes.

Do not allow any other text, imagery, or graphic element to enter the clear space zone.

### Minimum sizes

| Variant | Minimum rendered width |
|---|---|
| Icon | 24px |
| Wordmark | 120px |
| Full wordmark | 200px |

Below these sizes the circuit nodes and inner shield detail become illegible. Use the icon-only variant when space is very constrained.

### Approved color treatments

| Background | Logo treatment |
|---|---|
| White `#ffffff` | Full-color logo |
| Paper `#f7fbff` | Full-color logo |
| Navy `#0b4f8a` | Reverse: white shield lines + white text + green circuit nodes |
| Photography / imagery | Use only on light areas with sufficient contrast; prefer a white background lockup |

Do not place the logo on any background where the navy outer shield disappears or loses definition.

### Logo misuse

Do not:

- **Recolor** any element of the logo — the navy, blue, white, and green elements are fixed
- **Stretch or distort** the logo proportionally or non-proportionally
- **Add drop shadows, glows, or emboss effects** to the logo
- **Remove the circuit nodes** from the icon
- **Separate the "ASIS" text** from the shield icon
- **Recreate the logo in text** — do not represent OASIS with a plain-text "OASIS" styled to look like a logo
- **Place on busy or dark-patterned backgrounds** where the shield outline disappears
- **Rotate the logo** — the shield reads as a shield only when upright

---

## 10. UI Patterns

These patterns are defined in `src/index.css` and per-component CSS in the website project. Reference them for design consistency across any OASIS-branded interface.

### Buttons

Three button variants. All share: `border-radius: 8px`, `font-weight: 700`, `min-height: 42px`, `padding: 10px 20px`, transition on hover.

| Variant | Background | Text color | Border | Use |
|---|---|---|---|---|
| **Primary** | Green Bright `#4cd964` | Navy `#0b4f8a` | None | Primary CTA — "Join Team OASIS," registration submit |
| **Secondary** | Blue `#0f6fcf` | White | None | Secondary CTA — "See the model," navigation actions |
| **Outline** | Transparent | Blue `#0f6fcf` | 2px Blue | Tertiary / contextual links styled as buttons |

Button hover behavior: `opacity: 0.9` + `translateY(-1px)`. Active: `translateY(0)`.

Icons inside buttons use SVG with `stroke: currentColor`, `stroke-width: 2.25`, `stroke-linecap: round`, `stroke-linejoin: round`, size 17×17px.

### Badges

Pill badges for status, category, and principle tags. All use `border-radius: 100px`, `font-size: 0.78rem`, `font-weight: 600`, `letter-spacing: 0.04em`, `text-transform: uppercase`.

| Variant | Background | Text | Use |
|---|---|---|---|
| **Green** | `#e6faea` | `#1a7a2e` | Status: active, accepted, valid |
| **Blue** | Blue Soft `#e7f1ff` | Navy `#0b4f8a` | Category: credibility, problem/solution labels |
| **Purple** | `#ede9fe` | `#5b21b6` | Principle: Village; tool category tags |

The three principle badges map to the three guiding principles: Impact → Green, Credibility → Blue, Village → Purple.

### Icon style

All UI icons are SVG with:
- `fill: none`
- `stroke: currentColor`
- `stroke-width: 2` (2.25 in button contexts)
- `stroke-linecap: round`
- `stroke-linejoin: round`

Standard UI icon size: 21×21px. Button icon size: 17×17px. Do not use filled icons unless they are part of the logo or illustration set.

### Cards

Cards use `background: #ffffff`, `border: 1px solid var(--line)`, `border-radius: 8px`, `padding: 22px`. No drop shadows on standard cards — the border is sufficient. Use `var(--shadow)` only for elevated surfaces like the registration card.

### Section layout

- Standard section: `padding: 80px 0`
- Small section: `padding: 48px 0`
- Max content width: `1080px`, centered, `padding: 0 24px`
- Dark section (ethos/beliefs): `background: var(--ink)` (`#07111f`)

### Eyebrows

Section eyebrows (kickers above headings) use Geist Mono, 12px, 700 weight, `text-transform: uppercase`, `letter-spacing: 0.14em`.

- On light backgrounds: Blue `#0f6fcf`
- On dark (ink) backgrounds: Green Bright `#4cd964`

---

## 11. Writing Style

### Capitalization

- **OASIS** — always all-caps
- **AppSec** — capital A, capital S, no space; not "appsec," "app sec," or "App Sec"
- **GitHub** — capital G, capital H; never "Github" or "github"
- **OWASP** — always all-caps
- **Impact / Credibility / Village** — capitalize when used as OASIS principle names
- Section headings and page titles use **sentence case**, not Title Case
  - Correct: "How OASIS works"
  - Incorrect: "How OASIS Works"

### Headlines and headings

Use sentence case throughout. Capitalize proper nouns only. The three-line hero headline structure (*"Open source powers the world. Vibe hacking exploits it. Team OASIS fixes it."*) is the only exception — treat it as a proper branded phrase.

### Numbers

- Spell out one through nine in prose body copy
- Use numerals for 10 and above
- Use numerals always in UI labels, stats, step numbers, and tables
- Use a percent sign (50%) not "percent" in data contexts; spell out in prose ("fifty percent of attendees")

### Punctuation

- **Oxford comma** — always: "validators, project owners, and maintainers"
- **Em dashes** (—) for interruption and parenthetical phrases, with a space on each side; not en dashes (–) and not double hyphens (--)
- **Ellipsis** — use the single character (…) not three periods (...)
- **Quotes** — use curly/smart quotes in rendered output; straight quotes in code and markdown source

### Links and attribution

When referencing the project GitHub in external materials:

- Repository: `https://github.com/owasp-oasis/project-overview`
- Website: `https://www.owasp-oasis.org/`

Do not abbreviate the GitHub URL. Do not link to the repository without context — include a descriptor such as "the OASIS project documentation on GitHub."

### Press and attribution

When writing for press or third-party publications:

- First mention: **OASIS (Open Automated Security Initiative for Software)**
- Subsequent mentions: **OASIS**
- Do not describe OASIS as an OWASP project until formal approval is confirmed
- Acceptable factual context: *"OASIS has submitted a project proposal to OWASP."*

---

*Brand questions or proposed updates: open an issue in the [project-overview repository](https://github.com/owasp-oasis/project-overview).*
