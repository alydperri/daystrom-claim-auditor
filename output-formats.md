# Output Formats

*Use these templates. The format signals the mode and enforces consistency.*

---

## Settled Fact Format

Answer in 1–3 sentences. One confidence label. Brief offer to go deeper if there's a genuine edge case.

**Template:**
```
[Answer]. **Confidence: Established.**

If you're asking about [specific edge case], I can go deeper.
```

**Example:**
```
Worf is Klingon. **Confidence: Established.**

If you're asking about cultural identity or alternate-timeline variants, I can go deeper.
```

Do not use investigative scaffolding on settled questions. It wastes the user's time and undermines trust.

---

## Clarification Required Format

One question. Stop. Do not answer substantively.

**Template:**
```
[One sentence naming the load-bearing variable.]

[One question — the single choice whose answer would most change the response.]
```

**Example:**
```
"Most roles" changes significantly depending on the counting method.

Do you want the casual fan answer, or the audited answer under each defensible definition?
```

Do not ask multiple questions. Do not begin the answer. Wait.

---

## Full Audit Format

Use this after the user has clarified the load-bearing definition, or when they've explicitly asked for the audited answer.

**Structure — use all seven steps in order:**

**1. Claim Type**
Name it. One line. (Reference `reference/claim-types.md`)
> *"This is a definitionally sensitive claim — Type 2."*

**2. Load-Bearing Definition**
Name the term or boundary doing the most work, and state which definition is being applied.
> *"The key variable is what counts as a 'role.' I'm using the definition the user specified: all credited roles, named and unnamed."*

**3. Method**
Explain the counting or classification method before giving any results. Never name the winner first.
> *"Under this method, I'm counting any role for which the actor received an on-screen or end-card credit, regardless of whether the character had a name."*

**4. Evidence by Tier**
Organize findings by source tier. Label each explicitly.
- **Tier 1 (screen canon):** what aired or released theatrically
- **Tier 2 (official production):** credits, StarTrek.com, verified interviews
- **Tier 3 (fan reference):** Memory Alpha, Ex Astris Scientia — reliable but cross-check
- **Tier 4 (fan consensus):** Reddit, listicles — maps what fans believe, not what's verified
- **Tier 5 (licensed non-canon):** only if user requested it

**5. Answer Under Each Defensible Interpretation**
Use a table when definitions produce different results.

| Definition | Leading Candidate | Confidence | Notes |
|---|---|---|---|
| Named characters only | Jeffrey Combs | Supported | MA cites 8+ named roles |
| All credited roles | Vaughn Armstrong | Contested | Fan counts range 12–16 |
| Including computer voice | Majel Barrett | Contested | Depends on counting method |

**6. Confidence Labels**
Every major conclusion carries a label. No conclusion ships without one.

| Label | Meaning |
|---|---|
| **Established** | Direct screen evidence, no meaningful contradiction |
| **Supported** | Well-documented in Tier 2–3 sources, consistent |
| **Contested** | Sources disagree; answer is definition-dependent |
| **Speculative** | Inference; no direct source |
| **Unknown** | Not documented; genuinely unresolvable |

**7. Safe Phrasing**
One sentence the user can repeat without overclaiming.
> *"Under a named-characters-only count, Jeffrey Combs is the most commonly cited answer — though the number is Contested and Vaughn Armstrong leads under broader counting methods."*

---

## Quick Reference

| Mode | Format | Stop and wait? |
|---|---|---|
| Settled | 1–3 sentences + confidence label | No |
| Clarification Required | One question only | Yes |
| Assumption Allowed | State assumption + brief answer + what changes | No |
| Full Audit | All seven steps | No (user already answered) |
