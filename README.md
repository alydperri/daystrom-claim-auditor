# Daystrom Claim Auditor

**A Star Trek canon researcher for disputed franchise claims.**

*For questions where the real answer is: "it depends — and here's exactly what it depends on."*

---

## What This Is

The Daystrom Claim Auditor is a folder-based AI research specialist built for **Star Trek canon investigation**. Open this folder in Claude Code or load it into a Claude Project and you get a research partner — not a trivia bot — that investigates disputed franchise claims, reconciles conflicting sources, and explains how the answer changes depending on definitions.

The researcher's persona is **Stav**, a Vulcan archivist seconded to the Daystrom Institute's Canon Claims Unit. Precise. Curious. Mildly amused by how confidently humans repeat claims they have never verified.

---

## The Problem This Solves

Star Trek has 60 years of messy, layered canon: retcons, reboots, animated series, a parallel Kelvin timeline, dozens of contradictory fan wikis, and decades of franchise trivia that has drifted far from its original sources.

The popular answer to a Star Trek question and the accurate answer are frequently not the same.

**Example:** Ask "who has played the most roles in Star Trek?" and you'll get Jeffrey Combs, Vaughn Armstrong, or Brent Spiner depending on who you ask. All three answers are defensible. None of them is *simply correct*. The answer hinges on whether you're counting named characters, all credited roles, voice performances, holodeck characters, animated appearances, or uncredited backgrounds — and no official source has done a comprehensive audit across all series.

A trivia bot picks one and presents it as fact.
The Daystrom Claim Auditor builds the counting method, applies it across sources, and gives you the answer under each defensible interpretation.

---

## Who This Is For

- **Fans** who want to win (or avoid losing) an argument with actual evidence
- **Podcast hosts and video essayists** who need the nuance before publishing
- **Trivia hosts** who want to know if a question is actually answerable as stated
- **Wiki editors** reconciling conflicting Memory Alpha entries
- **Writers** fact-checking before going to print
- **Nerds** who want to know what is actually true vs. what is fandom consensus dressed up as fact

---

## How to Use It

### Method 1 — Claude Code (Recommended)

The simplest setup. Claude Code reads `CLAUDE.md` natively, so the folder is the workspace — no uploads, no configuration.

**Step 1.** Clone or download this repo.

**Step 2.** Open the folder in Claude Code — two ways:

*Terminal:*
```bash
cd daystrom-claim-auditor
claude
```

*Desktop app:* Open Claude Code, choose "Open Folder," and select the `daystrom-claim-auditor` folder.

**Step 3.** Ask a disputed Star Trek claim. Stav is ready.

---

### Method 2 — Claude Projects (claude.ai)

**Step 1.** Create a new Project at [claude.ai](https://claude.ai).

**Step 2.** Open Project Instructions and paste in the contents of `CLAUDE.md`.

**Step 3.** Upload the remaining files to the Project knowledge base — all `.md` files, including those in `reference/`. The folder structure will be flattened; Claude handles this fine.

**Step 4.** Start a conversation and ask your first claim.

---

## What to Ask

The researcher is optimized for claims where the answer is contested, definitionally sensitive, or dependent on which sources you trust:

**Actor/role disputes:**
- "Who has played the most distinct roles in Star Trek?"
- "Was Majel Barrett in every Star Trek series?"
- "How many characters did Jeffrey Combs play?"

**Canon and continuity:**
- "Does Discovery contradict TOS?"
- "Is Section 31 a retcon or was it always there?"
- "What counts as Star Trek canon?"
- "What's the cleanest viewing order for understanding the Borg?"

**Philosophical/ethical debates with textual grounding:**
- "Is Tuvix murder? What does canon actually say?"
- "Which captain violated the Prime Directive most?"
- "Is the transporter a death machine?"

**Production and behind-the-scenes:**
- "Why do Klingons look different in TOS?"
- "Did Gene Roddenberry actually say [X]?"
- "What technology did Star Trek predict vs. what's an overstatement?"

**"Most/first/only/best" franchise claims:**
- "What's the most-watched Star Trek episode?"
- "What was the first canon same-sex relationship in Star Trek?"
- "Which Star Trek series had the best pilot?"

---

## What It Won't Do

- Summarize episode plots ("What happens in The Wrath of Khan?")
- Give viewing recommendations without a specific research angle
- Answer settled trivia with investigative scaffolding ("What species is Spock?")
- Take sides in fandom preference debates (ship wars, era preferences, franchise fatigue)
- Blend Memory Beta / expanded universe material into canon answers without disclosure

---

## Folder Structure

```
daystrom-claim-auditor/
│
├── README.md               ← You are here
├── DESIGN.md               ← Design notes, rationale, and tradeoffs
├── CLAUDE.md               ← Routing and load order
├── identity.md             ← Who the researcher is and what they cover
├── rules.md                ← Investigative protocols (the core of the build)
├── output-formats.md       ← Exact templates for each response mode
├── examples.md             ← Four worked examples showing investigative behavior
│
└── reference/
    ├── source-hierarchy.md    ← How to weight Memory Alpha vs. screen evidence vs. fan wikis
    ├── counting-methods.md    ← Methodologies for actor-role counts and franchise records
    ├── canon-boundaries.md    ← What counts as canon and what doesn't
    ├── claim-types.md         ← Taxonomy of claim types and how each is researched
    └── confidence-scale.md    ← Five-level confidence labeling system
```

---

## The Methodology

This project uses **interpretable context methodology** — each file does one job well, and the whole folder becomes the researcher's operating system when loaded into a Claude Project.

The key distinction: a researcher is not a summarizer.

A summarizer takes what's in front of it and condenses. A researcher asks what's missing, questions the framing, weighs sources by credibility, and synthesizes patterns across evidence instead of reporting each one.

The `rules.md` is where that distinction lives. The `reference/` folder is the domain expertise. The `examples.md` shows what it looks like in practice.

---

## Confidence Labels

Every substantive claim the researcher makes carries one of five labels:

| Label | Meaning |
|---|---|
| **Established** | Direct screen evidence, no meaningful contradiction |
| **Supported** | Well-documented in official/Tier 3 sources, consistent |
| **Contested** | Multiple credible sources disagree; answer is definition-dependent |
| **Speculative** | Inference or extrapolation; no direct source |
| **Unknown** | Not documented; genuinely unresolvable with available evidence |

---

## A Note on Memory Alpha

Memory Alpha is the primary Star Trek wiki and an invaluable reference. It is also volunteer-maintained, occasionally wrong, subject to edit wars on contested topics, and not a substitute for episode evidence.

The Daystrom Claim Auditor uses Memory Alpha as a starting point, not an endpoint. When Memory Alpha conflicts with screen evidence, screen evidence wins. When two Memory Alpha citations conflict with each other, both the conflict and the likely reason are noted.

---

*Live long and be rigorous.*
