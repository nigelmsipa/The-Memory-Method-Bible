# The Memory Method Bible

A version-agnostic memorization framework for Scripture optimized for cognitive retention and thematic depth.

## What Is This?

The Memory Method Bible divides Scripture into meaningful **pericopes** (thematic units) that respect narrative boundaries and theological coherence. Rather than using arbitrary chapter/verse divisions, each unit is anchored to a memorable **Lore Title**—a thematic hook designed to trigger comprehensive recall.

This framework synthesizes:
- **Thematic unity** from the Toledot structure (Hebrew genealogical sections)
- **Manageable length** from the Parashot system (Jewish liturgical divisions)
- **Mnemonic power** through carefully crafted Lore titles based on theological commentary

## Project Structure

```
memory-method-bible/
├── data/
│   ├── base-structure/
│   │   ├── genesis-base.json          # Universal verse boundaries
│   │   ├── exodus-base.json           # (future)
│   │   └── ...
│   └── title-overlays/
│       ├── bsb/
│       │   ├── genesis-bsb.json       # Berean Study Bible titles
│       │   └── ...
│       └── kjv/
│           ├── genesis-kjv.json       # King James Version titles
│           └── ...
├── source-texts/
│   ├── BSB.txt                        # (reference texts, optional)
│   ├── KJV.txt
│   └── WEB.txt
└── README.md                          # This file
```

## How It Works

### Base Structure
Each `*-base.json` file contains the **universal, translation-agnostic pericope divisions**:
- Chapter and verse boundaries
- Pericope ID (e.g., GEN-001)
- Concept slug for programmatic use
- Thematic tags

Example:
```json
{
  "pericope_id": "GEN-001",
  "lore_title": "The Reservoir of Creation: New Order",
  "chapter_start": 1,
  "verse_start": 1,
  "chapter_end": 2,
  "verse_end": 3,
  "verse_count": 36,
  "concept": "creation_and_order",
  "tags": ["creation", "god_work", "order", "sabbath"]
}
```

### Title Overlays
Each translation-specific folder (e.g., `bsb/`, `kjv/`) contains **style-adapted titles**:
- **Lore Title**: The memory hook (identical across overlays)
- **Theme**: Translation-specific interpretation of the theological content

Example:
```json
{
  "pericope_id": "GEN-001",
  "title": "The Reservoir of Creation: New Order",
  "theme": "God's instant creative work establishing order from chaos and rest on the Sabbath."
}
```

## Genesis Overview

The Book of Genesis is divided into **30 pericopes**, organized by narrative and theological arc:

- **Units 1–9** (GEN-001 to GEN-009): Primeval History
  - Creation, Fall, Cain, Antediluvians, Flood, Covenant, Law, Babel

- **Units 10–18** (GEN-010 to GEN-018): Abraham Cycle
  - Call, Lot, Melchizedek, Covenant, Hagar, Hospitality, Lot's Escape, Akedah, Closure

- **Units 19–24** (GEN-019 to GEN-024): Isaac & Jacob Cycle
  - Esau's Birthright, Jacob's Ladder, Laban, Peniel, Purification, Esau's Genealogy

- **Units 25–30** (GEN-025 to GEN-030): Joseph Cycle
  - Rejection, Integrity, Prison, Elevation, Reconciliation, Vayechi

## Using This Framework

### For Memorization
1. Take the **base structure** file (e.g., `genesis-base.json`)
2. Choose your preferred **title overlay** (e.g., BSB or KJV)
3. Use the Lore Title as a memory hook via the **Method of Loci** (Memory Palace technique)
4. Associate each unit's theological theme with a location in your mental space
5. Practice sequential recall through your memory palace

### For Study
1. Open `genesis-base.json` to see all pericope boundaries and thematic tags
2. Reference the translation overlay of your choice for specific theological wording
3. Use chapter:verse references to locate text in your own Bible

### For Development
1. Combine base structure with overlay to generate annotated Scripture documents
2. Create Bible reading apps with pericope-based navigation
3. Build memorization tools (flashcards, spaced repetition, etc.)
4. Generate custom Bible study formats

## Current Progress

### Completed
- ✅ Genesis (30 pericopes)
  - ✅ Base structure
  - ✅ BSB overlay
  - ✅ KJV overlay

### Planned
- ⬜ Exodus
- ⬜ Leviticus
- ⬜ Numbers
- ⬜ Deuteronomy
- ⬜ Joshua through Revelation (60+ additional books)

## Theological Framework

The Memory Method Bible is built on several key principles:

1. **Thematic Unity**: Each pericope respects narrative boundaries and theological concepts
2. **Cognitive Science**: Units are sized (typically 20–100 verses) to optimize working memory
3. **Lore as Anchor**: Titles function as powerful mnemonic triggers, encoding meaning into memory
4. **Translation Flexibility**: Base structure works with any translation; overlays adapt titles to specific styles
5. **Historical Fidelity**: All divisions maintain precise cross-reference with standard chapter:verse numbering

## License

- **Base structures** (`*-base.json`): CC0 (Public Domain)
- **Title overlays** (`*-*.json`): CC BY-SA 4.0 (Attribution + Share-Alike)
- **Bible texts**: See individual translation licenses
  - BSB: CC BY-SA 4.0
  - KJV: Public Domain
  - WEB: Public Domain

## Contributing

To contribute additional translations or pericope divisions:
1. Maintain the JSON schema exactly as specified
2. Ensure all pericope_ids reference corresponding base structure entries
3. Provide thoughtful, translation-appropriate titles and themes
4. Test JSON validity before submission

## References

- Toledot structure: *Genesis* Wikipedia article
- Parashah divisions: Chabad.org, "Weekly Torah Portion"
- Cognitive science of memorization: NIH PMC research on chunk limits and recall
- Theological commentary: Ellen G. White commentary and theological sources

## Questions?

This framework is designed to be self-documenting through its JSON structure. Each file is human-readable and machine-parseable.

For implementation questions or feedback, please refer to the project documentation or create an issue.

---

**The Memory Method Bible**: Transforming Scripture from sequential text into a structured, memorable, theological map.
