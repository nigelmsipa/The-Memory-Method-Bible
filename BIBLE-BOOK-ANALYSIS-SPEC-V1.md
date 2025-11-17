# Bible Book Analysis Spec Sheet
**Systematic Approach – Version 1.0**
(As finalized in development)

## Goal
Create a non-arbitrary, memorization-friendly, literary-sensitive hierarchical outline of any Bible book that serves two projects:

1. **Bible Memory Method** (deep-research tool / future app)
2. **Wolf and Words** (memorization app that will later pull simplified chunks from this system while keeping traditional chapters/verses)

## Core Principles (never break these)
1. Divisions must be justified by the text itself (flow, speaker change, resolution, literary device, chiasm hinge, inclusio, shift in topic/time/audience, etc.).
2. Nothing is arbitrary. Every cut gets a short, plain-English "why this starts/ends here + literary glue".
3. We are translation-agnostic. The scaffolding works with KJV, ESV, NIV, French Louis Segond, etc.
4. Traditional chapter-verse numbers are preserved in metadata (never hidden from the user, just not visually dominant in reading mode).

## Fixed Hierarchy (always this order)
```
Book
├─ Hebrew Name + English Name
├─ Canonical Grouping (Torah, Major Prophets, Writings, Gospel, Pauline, etc.)
├─ Big-Picture Literary Notes (overall chiasm, repeated refrains, non-chronological arrangement, etc.)
└─ Stories (self-contained arcs that advance the book's narrative)
   └─ Scenes (memorizable beats/pericopes, naturally determined by text)
```

**NOTE ON THEMES:** Themes are optional scaffolding that can be imposed later if desired. Stories and scenes are the core building blocks and take priority.

## Required Fields at Each Level

**Story level**
- Story letter (A, B, C, etc.)
- Story title (memorable & accurate)
- Why it starts here
- Why it ends here
- Literary glue / devices that hold it together (chiasm, parallelism, repetition, metaphor, inclusio, allusion, irony, hyperbole, wordplay, etc.)
- Traditional reference range

**Scene level**
- Scene number (1, 2, 3, etc.)
- Scene title (short, vivid when possible)
- Why it starts here
- Why it ends here (thought resolves, speaker changes, image completes, divine speech ends, etc.)
- Key literary devices at play in this exact scene
- Traditional verse range

### Critical: Scene Definition
A scene is **one complete, memorizable thought**. It is not a forced chunk of arbitrary length. The text itself determines where scenes naturally end:
- Thought completion
- Speaker change
- Resolution of a narrative arc
- Shift in time/place/action
- Natural pause in the text's flow

## Title Styles (for Bible Memory Method app)
User chooses one style globally per session:

1. **Plain** (neutral, modern, factual)
   → "Indictment of Judah"
2. **Evocative** (punchy, memorable, slightly dramatic)
   → "God Roars at His Rebellious Children"
3. **Archaic** (KJV-era poetic feel)
   → "The Lord's Controversy with His People"

Metadata explanations always stay Plain English (clarity > style when studying).

## Two Modes in the Final Product

**Reading / Orientation Mode**
Only titles are visible (Story → Scene) + text.
Acts as guardrails / mental map.
No verse numbers prominent.

**Study / Deep Mode** (toggle on)
All metadata appears:
- Why start/end
- Literary devices
- Traditional chapter-verse range
- Cross-references, allusions, wordplay notes
- Hebrew/Greek key terms when helpful

## Output Format (exact template we use for every book)

```
Book of [English Name] (Hebrew: [Name])
Grouping: [e.g., Torah]
Big-picture notes: [2–4 sentences max on overall structure/themes]

- Story A: [Title]
  → Why start/end + literary glue: [plain English]
  → Reference: [chapters:verses]
  - Scene 1: [Title]
    → Why start/end + devices: [plain English]
    → Reference: [verses]
  - Scene 2: [Title]
    → Why start/end + devices: [plain English]
    → Reference: [verses]
  - Scene 3: [Title]
    → Why start/end + devices: [plain English]
    → Reference: [verses]

- Story B: [Title]
  → Why start/end + literary glue: [plain English]
  → Reference: [chapters:verses]
  - Scene 1: [Title]
    → Why start/end + devices: [plain English]
    → Reference: [verses]
  - Scene 2: [Title]
    → Why start/end + devices: [plain English]
    → Reference: [verses]
```

## Workflow Going Forward
1. Pick the book.
2. Use AI prompt (see GENESIS-PROMPT.md for template) to generate stories and scenes.
3. Let the TEXT determine story and scene count—no arbitrary minimums or maximums.
4. Each scene must be a complete thought; don't force-fit into predetermined chunks.
5. Review/adjust if needed.
6. Approved version becomes the master scaffold for both apps.

## Key Commits & History
- **v1.0**: Initial spec finalized after Jeremiah V1 and new structure exploration
- Simplified from theme-heavy approach to story/scene-first methodology
- Focus on shipping over perfectionism
- Translation-agnostic, text-driven boundaries

---

**This spec is locked. Use it for all future Bible book outlines.**
