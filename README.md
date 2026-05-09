https://justinsteinmetz.github.io/RPGFLIFE-/

# RPG4LIFE

**An identity instrument for Grades 11–12.**

> Some roles were assigned. Some were chosen. Most became part of you through repetition.

---

## Concept

RPG4LIFE reframes identity as a character build — assembled from roles inherited before conscious choice, roles selected under social constraint, and scripts repeated until they feel like personality.

The central question: **what feels like personality, and what is a role you have levelled through repetition?**

The instrument uses the language and visual grammar of role-playing games not as decoration but as structural argument: identity is not a fixed essence. It is a build. Builds can be examined. Some elements are assigned. Others are chosen. The distinction matters.

---

## The core structural distinction

Every element of the character sheet is colour-coded and tagged:

| Type | Colour | Meaning |
|---|---|---|
| **Assigned** | Amber | Inherited, given, not chosen — present before consent |
| **Chosen** | Cyan | Built, selected, developed over time |

This distinction is the conceptual core of the instrument. It is enforced visually at every level — card borders, stat bars, input borders, badge labels. Students absorb it before they've read a single prompt.

---

## The character sheet

Six sections, partly pre-filled, partly student-completed.

### 1. Primary Class (Assigned)
Eight family and birth-order roles — students select one that fits their assigned family position. Each card carries a 16×16 pixel-art icon and a one-line description of the role's structural implication.

| Class | Core implication |
|---|---|
| Eldest Child | Responsibility assigned before consent |
| Youngest Child | Indulged or overlooked — the role of becoming |
| Only Child | Undivided attention; undivided expectation |
| Middle Child | The negotiator — identity built in the gap |
| Caretaker | Assigned emotional or practical responsibility for others |
| Outsider | Placed outside the group before choosing to leave it |
| The Achiever | Success as the primary assigned identity |
| The Rebel | Resistance as role — opposition as definition |

### 2. Secondary Classes (Chosen)
Twelve social and identity roles — students select up to three. Leader, Helper, Performer, Scholar, Protector, Skeptic, Creator, Diplomat, Loner, Connector, Idealist, Realist. Each carries a pixel-art icon.

### 3. Base Stats (Assigned)
Four stats set by early experience — Trust, Autonomy, Belonging, Visibility. Students drag sliders to reflect how these actually landed, not how they were intended. Amber bars.

### 4. Developed Stats (Chosen)
Four stats built over time — Resilience, Empathy, Ambition, Boundaries. Cyan bars.

### 5. Inventory, Buffs & Debuffs
Two-part each: what was given (assigned) and what was acquired (chosen). The buff/debuff pair is the most analytically revealing entry on the sheet — it forces students to name both an advantage their build provides and a hidden cost it carries.

### 6. Active Quest & Respec
What the student is currently working toward, and what they are trying to change about their build. The respec entry is where the instrument touches revision — what a student names here, and what is making the change difficult, is primary data for the AI reading.

### The Core Question
The final field — minimum 30 characters: *"Which parts of this build feel like you — and which parts feel like a role you levelled into?"* The most important entry on the sheet. The AI prompt is instructed to quote or reference the student's specific language here.

---

## The pixel art icons

All 20 class cards carry hand-drawn 16×16 SVG pixel art icons built on a strict pixel grid with `shape-rendering="crispEdges"`. Icons use `currentColor` and inherit amber (assigned) or cyan (chosen) from their card context automatically. No additional JS required.

Each icon is designed to be immediately readable as an archetype: crown (Eldest), lightning bolt (Rebel), broken circle (Outsider), moon (Loner), linked nodes (Connector), question mark (Skeptic).

---

## The build analysis

After the sheet is completed, the model reads it as a structural analysis — not a personality description.

**What the model reads for:**
- The relationship between the assigned primary class and the chosen secondary classes. Does the student's chosen build reinforce the assignment, resist it, or compensate for it?
- The stat pattern — Low Trust + High Resilience tells a different story than High Trust + Low Boundary.
- The buff/debuff pair — what it reveals about who pays the cost of this build and who benefits.
- The respec entry — what the student is trying to change, and what the sheet suggests is making that difficult (even if the student hasn't named it).
- The core question — quoted or referenced directly.

**Output:** headline (4–8 words, names the central structural feature of the build), reading (200–270 words, structural analysis), signature (one sentence — the most specific thing the build reveals about what has become second nature versus what remains a performance), three discussion questions derived from the sheet specifically.

**The model does not describe personality.** It analyses structure. The distinction is enforced in the prompt rules.

---

## Design

**Aesthetic** — terminal green on near-black. Scanlines. Vignette. The Rajdhani typeface is military/technical without being fantasy. The green glow on the title flickers subtly. The overall feel is a real diagnostic system, not a game parody.

**The result screen breaks entirely** — warm paper background, DM Serif Display, no scanlines. The register shift signals that the game frame has ended and the analysis has begun.

**Restart is labelled "Respec →"** — the RPG language is consistent throughout.

**Session ID** — `RPG-XX-XX` format, carried through to the result stamp.

---

## Pedagogical notes

**This is not a lesson about gaming.** The RPG framing is a Trojan horse. Students engage with a character sheet before they realise they are doing serious self-examination. The AI reading is the moment the frame drops.

**The assigned/chosen distinction does the structural work.** The instrument makes visible — without stating it directly — that many traits experienced as personality were installed before the student could consent to them. The distinction between the amber and cyan sections is the lesson.

**The buff/debuff pair is the hardest entry.** Naming a hidden cost of your own build requires both self-awareness and honesty. Students who answer this well produce the most revealing portraits.

**The respec entry is optional in tone but critical in data.** If a student leaves it thin or vague, the AI portrait should name what the sheet suggests they are trying to change even if they haven't said so directly.

**The result is private by default.** Students choose what, if anything, leaves the room.

**Discussion entry points** (generic — the instrument generates three specific ones per student):
- "Does your primary class feel like an accurate description of the role you were assigned — or does it miss something?"
- "Which secondary class did you hesitate over? Why?"
- "Name a trait that feels genuinely yours. Now trace where it came from."
- "The build analysis named something. Is it accurate — and if it's wrong, why might it be wrong in that specific way?"
- "What would a full respec cost you — socially, practically, personally?"

---

## Abitur Themenfeld relevance

| Themenfeld | Angle |
|---|---|
| The Individual & Society | Identity formation, social roles, conformity vs. individuality, the construction of the self through repetition |
| Science & Technology | Gamification of identity; the RPG as structural metaphor for how systems assign and shape roles |

---

## Suite relationship

RPG4LIFE is designed as a precursor to **SOCIAL CONTRACT** (planned) — a civic simulation instrument where students inhabit randomly generated character profiles and face dilemmas from those positions. In that sequence:

- RPG4LIFE: you examine your own build
- SOCIAL CONTRACT: you inhabit someone else's build and discover that the rules of the civic game land differently depending on starting stats

The contrast between the two sessions is where the structural critique of inequality becomes legible.

---

## Technical architecture

Uses the same Cloudflare Worker proxy as the rest of the suite.

```javascript
const PROXY = "https://anthropic-proxy.justin-steinmetz.workers.dev";
```

One API call per session — the build analysis at the end. See the *Who Are You, Really* README for full Worker deployment instructions.

### Deployment

Single HTML file. No dependencies, no build step. Rename `rpg4life.html` to `index.html` and push to a GitHub Pages repository.

