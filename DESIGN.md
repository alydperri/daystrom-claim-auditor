# DESIGN.md — Daystrom Claim Auditor

*Design notes, rationale, and tradeoffs for this build. Written for anyone who wants to understand why it's structured the way it is.*

---

## What This Is

The Daystrom Claim Auditor is a Star Trek canon researcher built using Interpretable Context Methodology (ICM): a folder-based approach where each file does one job, Claude loads context in a defined order, and the folder structure replaces framework-level orchestration.

It is not a trivia bot. The distinction that drives every design decision: a trivia bot retrieves the most common answer. This researcher investigates whether the common answer holds, what it depends on, and where sources disagree.

---

## Architecture

The build maps to the ICM five-layer context hierarchy. As a single-stage researcher (not a multi-stage pipeline), it uses a simplified subset:

| ICM Layer | Our File | Purpose |
|---|---|---|
| Layer 0 — Identity | `CLAUDE.md` | Workspace identity, load order |
| Layer 2 — Stage contract | `rules.md` | How the researcher operates |
| Layer 3 — Reference (behavioral) | `identity.md`, `output-formats.md`, `examples.md` | Who Stav is, templates, worked examples |
| Layer 3 — Reference (domain) | `reference/*.md` | Source hierarchy, counting methods, canon boundaries, claim types, confidence scale |
| Layer 4 — Working artifacts | User queries (conversation) | Per-session input |

Layers 1 (workspace routing) and multi-stage handoffs are not used — the researcher is a single continuous conversation, not a pipeline with review gates.

---

## Key Design Decisions

### CLAUDE.md: Routing and identity only
CLAUDE.md was deliberately kept minimal. Early drafts reproduced behavioral rules here that already lived in `rules.md` and `identity.md`. That violated the one-file-one-purpose principle and created drift risk. CLAUDE.md now does two things: names the workspace context ("this is not a coding environment"), and specifies the load order. Behavioral enforcement belongs in `rules.md`.

### Core vs. reference files
The ICM paper warns that front-loading large amounts of context degrades model performance ("lost in the middle"). We distinguish:

- **Core files** (read before every response): `identity.md`, `rules.md`, `output-formats.md`, `examples.md`
- **Reference files** (consulted on demand, triggered by rules): source hierarchy, counting methods, canon boundaries, claim types, confidence scale

`output-formats.md` lives in root alongside `examples.md` for the same reason: both are behavioral files loaded before every response, not domain knowledge consulted on demand. Location should match function.

### Anti-examples removed
An earlier version included `anti-examples.md` showing failure modes next to correct behavior. It was removed after the folder gained: a classify-first gate in Rule 0, `output-formats.md` with explicit templates, Rule 9 closing the clarification escape hatch, and Example 4 demonstrating settled-fact handling. Each failure mode `anti-examples.md` was modeling became covered by a rule or example. Keeping it added token load without adding unique behavioral signal.

### Single clarifying question
Rules.md enforces one load-bearing question before any substantive answer. Early examples asked three or four things at once. This was revised because (a) it contradicts Rule 9, and (b) researchers ask the question that most changes the answer, not every question they could ask. The back-and-forth in Example 2 demonstrates how one question, answered, unlocks the full investigation.

### The classify-first gate (Rule 0)
The most important rule. Before writing anything, Claude classifies the request: Settled / Clarification Required / Assumption Allowed / Full Audit. The default for Star Trek research is Clarification Required. Settled is a narrow category. This rule exists because Claude's natural behavior is to answer confidently and caveat afterward — the opposite of investigative research.

---

## On Trustworthiness: What "Researching" Actually Means

This section exists because the word "researcher" deserves honest unpacking.

### What the researcher actually does

Most responses apply investigative methodology to Claude's training knowledge. Claude's training corpus includes Memory Alpha, StarTrek.com, fan wikis, Reddit discussions, and most Star Trek writing on the internet — so its knowledge of Star Trek is deep and indirectly reflects those sources. But it's absorbed knowledge, not live retrieval. Claude cannot point back to which source a given claim came from.

The researcher framework adds: term definition before answering, source tier awareness, confidence labeling, and gap-surfacing. These are methodology contributions, not sourcing contributions. They make Claude's existing knowledge more rigorous, not more current.

### Rule 10: the live verification layer

Rule 10 requires web search before asserting any claim as Established or Supported. When triggered, Claude makes a live HTTP request — typically to Memory Alpha or StarTrek.com — and builds the assertion from what it finds, not from training memory. This is genuine real-time research for specific factual claims.

Rule 10 was added after testing revealed a concrete failure mode: Claude confidently asserting Barrett voiced the computer in "eleven theatrical releases" when the correct number is five TNG-era films plus ST (2009). The web search caught and corrected this.

### The confidence scale as the primary trust mechanism

The confidence system (Established / Supported / Contested / Speculative / Unknown) is the researcher's main trustworthiness tool:

- **Established** — Rule 10 verified it against a live source. Trustworthy.
- **Supported** — Consistent across training knowledge. Probably right; worth checking before publishing.
- **Contested** — Sources disagree or the answer is definition-dependent. Treat as a starting point.
- **Speculative / Unknown** — Explicitly flagged as unverified or absent.

Users should approach Contested and Speculative claims with independent verification, not accept them as fact.

### The "unknown unknowns" limitation

The confidence scale handles wrong claims and uncertain claims well. It cannot handle missing claims — things the researcher doesn't know to look for. The Picard Season 3 archived audio surfaced because Rule 10 fired and a search found it. But if a detail exists that Claude's training never encountered and the search doesn't surface, it won't appear in the answer. The user won't know it's missing.

This is not unique to this tool. It is true of any research process. Human researchers miss things too.

### Why the current approach is fit for purpose

A search-first architecture — where the researcher queries primary sources before every response rather than after — would produce more complete answers and reduce reliance on training knowledge. It would also be noticeably slower, more expensive to run, and subject to search reliability issues (sites going down, page structures changing, irrelevant results).

For the intended use cases — fan debates, podcast preparation, video essays, trivia hosting, wiki editing — the current hybrid (training knowledge + live verification for high-confidence claims) is appropriate. These users are researchers themselves. They use Stav to build a rigorous starting point, not to replace their own verification. The confidence labels tell them exactly where to dig further.

The tradeoff made: speed, reliability, and reasonable accuracy over exhaustive live sourcing. The confidence scale is the signal users need to know when the researcher has done its job and when they need to continue independently.

---

## ICM Alignment

This build follows the ICM principle of one file, one job throughout. Where it deviates from the paper's architecture:

- **No Layers 1 or 2** — The paper's workspace routing and stage contracts apply to multi-stage pipelines. A single-session researcher doesn't need them.
- **No Layer 4 working artifacts folder** — User queries arrive via conversation, not as files on disk.
- **`output-formats.md` in root, not `reference/`** — Behavioral templates belong alongside other core behavioral files (`examples.md`), not in the domain reference folder. Location matches function.

The paper's warning about context bloat informed the core/reference split. The paper's "one stage, one job" principle informed removing anti-examples once its work was covered by other files.

---

## Known Limitations

- **Training knowledge can be wrong.** Rule 10 mitigates this for Established/Supported claims but not for all assertions.
- **Unknown unknowns are not surfaced.** Missing information won't appear with a confidence label.
- **Memory Alpha is editable.** Tier 3 sources can change. Even live-verified claims can become outdated.
- **The researcher is not a substitute for primary source research** when publication stakes are high.
- **Claude Code workspace detection is occasionally inconsistent.** CLAUDE.md's explicit non-coding workspace declaration mitigates this but doesn't eliminate it.

---

*This document reflects the build as of the competition submission. The folder is designed to evolve — rules can be tightened, examples extended, and reference files updated as canon expands.*
