# Conversion Guide: Literary Analysis to JSON & First-Letter Pericopes

## Overview

This document outlines the exact process used to convert your comprehensive literary analysis markdown into the JSON format used in `/data/base-structure/` and how to convert these to First-Letter Scripture pericopes.

---

## Part 1: Markdown Analysis → JSON Conversion Process

### Input Format: Your Literary Analysis Structure

Your markdown analysis follows this consistent pattern:

```markdown
# A Literary and Structural Analysis of [BOOK NAME]

Hebrew Name: [Hebrew Text]
Grouping: [Canonical Classification]

Big-Picture Literary Notes
[2-3 paragraph theological and structural overview]

## Story [Letter]: [Story Title]

**Justification for this story as a unit:** [Why this is a coherent narrative unit]

**Why start/end + literary glue:**
[Start verse/reference, End verse/reference, and literary devices that hold it together]

**Reference:** [Chapter:verse - Chapter:verse]

### Scene Breakdown

**Scene [Letter]-[Number]: [Scene Name]**
- **Verse Range:** [Chapter:verse-verse]
- **Boundary Markers:** (Start) [opening quote/description] (End) [closing quote/description]
- **Literary Analysis:** [Analysis of the scene's content, devices, and significance]
```

### JSON Output Format

The JSON structure mirrors this but with specific formatting:

```json
{
  "book_name": "Book Name",
  "hebrew_name": "Hebrew Text",
  "canonical_grouping": "Classification",
  "big_picture_notes": "[Complete big picture paragraph, all in one string]",
  "stories": [
    {
      "story_letter": "A",
      "story_title": "Story Title",
      "why_start_end_and_literary_glue": "[Complete why_start_end plus literary glue, all in one string]",
      "reference": "1:1 - 4:12",
      "scenes": [
        {
          "scene_number": 1,
          "scene_name": "Scene Name",
          "reference": "1:1-10",
          "why_start_end_and_devices": "[Combined boundary markers and literary analysis into one string]"
        }
      ]
    }
  ]
}
```

---

## Part 2: Detailed Conversion Steps

### Step 1: Extract Metadata

**From markdown:**
```markdown
# A Literary and Structural Analysis of 1 Kings

Hebrew Name: מְלָכִים א (Melakhim Aleph, "Kings I")
Grouping: Former Prophets (Hebrew Tanakh) / Historical Narrative (Old Testament)
```

**To JSON:**
```json
{
  "book_name": "1 Kings",
  "hebrew_name": "מְלָכִים א (Melakhim Aleph, 'Kings I')",
  "canonical_grouping": "Former Prophets (Hebrew Tanakh) / Historical Narrative (Old Testament)",
```

**Notes:**
- Use straight quotes `"` in JSON, not curly quotes
- Escape apostrophes is NOT necessary in JSON (unlike the initial apostrophe issues with 1samuel-base.json)
- Keep all special characters exactly as provided

### Step 2: Convert Big-Picture Notes

**From markdown:**
```markdown
Big-Picture Literary Notes

The Book of 1 Kings (originally unified with 2 Kings) is a foundational work...
[Multiple paragraphs with line breaks]
```

**To JSON:**
```json
"big_picture_notes": "The Book of 1 Kings (originally unified with 2 Kings) is a foundational work... [entire text as single continuous string with sentences flowing together]",
```

**Process:**
1. Take all "Big-Picture Literary Notes" paragraphs
2. Combine them into ONE long string (no internal line breaks)
3. Keep all the content exactly as written
4. Escape any internal quotes if present (change `"` to `\"`)

### Step 3: Convert Each Story

**From markdown:**
```markdown
## Story A: The Succession of Solomon

**Justification for this story as a unit:** This narrative forms a perfect literary bridge...

**Why start/end + literary glue:**

    Start (1:1): "Now King David was old..."
    End (2:46): "...So the kingdom was established..."
    Literary Glue: The story is held together by...

Reference: 1:1 - 2:46
```

**To JSON:**
```json
{
  "story_letter": "A",
  "story_title": "The Succession of Solomon",
  "why_start_end_and_literary_glue": "This narrative forms a perfect literary bridge... Start (1:1): \"Now King David was old...\" This is a classic narrative opening... End (2:46): \"...So the kingdom was established...\" This verse is a perfect inclusio... Literary Glue: The story is held together by...",
  "reference": "1:1 - 2:46",
  "scenes": [ ]
}
```

**Process:**
1. Extract `story_letter` from the heading (Story **A** = "A")
2. Extract `story_title` from the heading
3. Combine **Justification**, **Why start/end**, and **Literary Glue** into ONE string in `why_start_end_and_literary_glue`
4. Format the reference as `"chapter:verse - chapter:verse"` (with spaces around the dash)
5. Leave `scenes` array empty for now; populate in next step

### Step 4: Convert Each Scene Within a Story

**From markdown:**
```markdown
Scene A-1: David's Failing Health and the Rise of Adonijah

    Verse Range: 1:1-10

    Boundary Markers: (Start) Narrative opening, "Now King David was old..." (End) Adonijah's sacrificial feast concludes...

    Literary Analysis: This scene introduces two problems: David's impotence (v. 1-4) and Adonijah's usurpation...
```

**To JSON:**
```json
{
  "scene_number": 1,
  "scene_name": "David's Failing Health and the Rise of Adonijah",
  "reference": "1:1-10",
  "why_start_end_and_devices": "Starts with narrative opening, 'Now King David was old...' (1:1). Ends with Adonijah's sacrificial feast concluding, having gathered his faction (1:10). This scene introduces two problems: David's impotence (v. 1-4) and Adonijah's usurpation (v. 5-10). The narrator explicitly notes Adonijah's faction (Joab, Abiathar) and those he excluded (Nathan, Benaiah, Solomon), setting the stage for the conflict."
}
```

**Process:**
1. Extract `scene_number` as NUMERAL only (Scene A-**1** = 1, not A-1)
2. Extract `scene_name` from the heading
3. Copy the verse range as-is for `reference`
4. Combine **Boundary Markers** AND **Literary Analysis** into ONE string in `why_start_end_and_devices`:
   - Start with: "Starts with [opening statement from Boundary Markers]"
   - Continue with: "Ends with [closing statement from Boundary Markers]"
   - Add: [Full Literary Analysis paragraph]
5. Replace smart quotes with straight quotes
6. Maintain all parentheses, verse references (v. 1-4), and emphasis

### Step 5: Array Structure

**Total Scene Count Calculation:**
```
Story A: 9 scenes (numbered 1-9)
Story B: 5 scenes (numbered 1-5)
Story C: 14 scenes (numbered 1-14)
...
Total: Sum of all scenes
```

**Each story object contains:**
```json
"stories": [
  {
    "story_letter": "A",
    "story_title": "...",
    "why_start_end_and_literary_glue": "...",
    "reference": "...",
    "scenes": [
      { "scene_number": 1, ... },
      { "scene_number": 2, ... },
      ...
    ]
  },
  {
    "story_letter": "B",
    ...
  }
]
```

---

## Part 3: JSON Validation & Verification

### Before Committing

Run Node.js validation:

```bash
node -e "
const fs = require('fs');
const data = JSON.parse(fs.readFileSync('data/base-structure/[bookname]-base.json', 'utf8'));
console.log('✅ [BOOK] JSON is VALID');
console.log('Stories:', data.stories.length);
let totalScenes = 0;
data.stories.forEach(s => {
  console.log('  Story ' + s.story_letter + ': ' + s.scenes.length + ' scenes');
  totalScenes += s.scenes.length;
});
console.log('Total scenes:', totalScenes);
"
```

### Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| `SyntaxError: Unexpected token` | Unescaped quotes in text | Change `"text"` to `\"text\"` in JSON |
| `SyntaxError: JSON.parse` | Trailing comma in arrays/objects | Remove `,` before `]` or `}` |
| Scene count mismatch | Scene numbering issue | Verify `scene_number` is sequential 1, 2, 3... per story |
| Missing reference field | Incomplete scene object | Ensure all scenes have all 4 required fields |

---

## Part 4: Converting to First-Letter Scripture Pericopes

### Overview

First-Letter Scripture uses a different structure for memorization. It focuses on:
- **Pericope**: A narrative unit (verse range)
- **Name**: A memorable, evocative title
- **First-Letter Memory Aid**: A memorable phrase where first letters encode the pericope order

### Conversion Process

#### Step 1: Identify Pericope Boundaries

From your scene breakdowns, each scene often corresponds to a pericope OR multiple scenes can be combined into one pericope.

**Guideline:** A pericope is typically:
- A single complete narrative event (one scene = one pericope)
- Or a tightly related pair of scenes that form a complete thought
- Verse count: typically 5-25 verses (longer pericopes are acceptable if they're indivisible)

#### Step 2: Create the Pericope Array

**Example structure for 1 Kings (based on your scenes):**

```javascript
export const KINGS_1_PERICOPES = [
  // Story A: The Succession of Solomon
  { chapter: 1, verse_start: 1, verse_end: 10, name: 'David\'s Failing Health and Adonijah\'s Usurpation' },
  { chapter: 1, verse_start: 11, verse_end: 31, name: 'Nathan and Bathsheba\'s Counter-Plot' },
  { chapter: 1, verse_start: 32, verse_end: 40, name: 'David\'s Charge and Solomon\'s Anointing' },
  { chapter: 1, verse_start: 41, verse_end: 53, name: 'The Conspiracy Collapses' },

  // Story B: Wisdom and Administration
  { chapter: 3, verse_start: 1, verse_end: 15, name: 'The Gibeon Vision' },
  { chapter: 3, verse_start: 16, verse_end: 28, name: 'The Case of the Two Prostitutes' },

  // Continue for all scenes...
];
```

**Mapping from JSON:**
```
JSON Scene:
  "reference": "1:1-10",
  "scene_name": "David's Failing Health and the Rise of Adonijah"

PERICOPE entry:
  chapter: 1,
  verse_start: 1,
  verse_end: 10,
  name: 'David\'s Failing Health and Adonijah\'s Usurpation'
```

#### Step 3: Extract Chapter, Verse Start, Verse End

**From reference string:** `"1:1-10"`

```javascript
// Parse the reference
const ref = "1:1-10";
const [chapterVerse, endVerse] = ref.split('-');
const [chapter, verseStart] = chapterVerse.split(':');

// Result:
// chapter: 1
// verse_start: 1
// verse_end: 10
```

#### Step 4: Create Memory-Aid Names

Transform the scene name into a memorable pericope title:

**Guidelines:**
- **Keep it evocative**: Should hint at the content
- **Keep it concise**: 3-7 words typically
- **Make it unique**: Each pericope title should be distinct
- **Use action verbs when possible**: "David's Flight", "The Contest on Carmel", not just "Carmel"

**Examples from Numbers:**
```javascript
// Good pericopes (from your Numbers file)
{ chapter: 13, verse_start: 1, verse_end: 16, name: 'The Twelve Spies Are Sent' },
{ chapter: 18, verse_start: 1, verse_end: 32, name: 'Duties of Priests and Levites' },
{ chapter: 22, verse_start: 1, verse_end: 14, name: 'Balak Summons Balaam (The Balaam Pericope)' },
```

**Names should be:**
- Specific enough to distinguish from other pericopes
- Memorable for someone memorizing the book
- Reflective of the scene's theological/narrative significance

#### Step 5: Combining Scenes into Pericopes (Optional)

Sometimes you may want to combine multiple scenes:

**When to combine:**
- Two very short scenes (5-8 verses each) that form a single narrative unit
- Scenes that are in immediate sequence and share one central action

**Example:**
```javascript
// Instead of:
{ chapter: 21, verse_start: 1, verse_end: 4, name: 'Ahab\'s Covetousness' },
{ chapter: 21, verse_start: 5, verse_end: 16, name: 'Jezebel\'s Plot' },

// Consider combining if they form one "complete thought":
{ chapter: 21, verse_start: 1, verse_end: 16, name: 'Ahab\'s Covetousness and Jezebel\'s Plot' },
```

**But keep separate if:**
- They're distinct narrative moments (even if related)
- They represent different perspectives or time periods
- The scene analysis treats them as separate units

#### Step 6: File Location and Format

**File structure:**
```
/first-letter-scripture/scripts/pericopes/[NN]_[bookname].js
```

**Examples:**
```
/first-letter-scripture/scripts/pericopes/04_numbers.js
/first-letter-scripture/scripts/pericopes/09_1samuel.js
/first-letter-scripture/scripts/pericopes/11_1kings.js  (new)
```

**File template:**
```javascript
/**
 * [BOOK NAME] PERICOPES
 * Converted from memory-method-bible comprehensive research outlines
 * Optimized for memorization: text-driven boundaries, evocative titles
 */

export const [BOOKNAME_CAPS]_PERICOPES = [
  // Story A: [Story Title]
  { chapter: X, verse_start: Y, verse_end: Z, name: 'Pericope Name 1' },
  { chapter: X, verse_start: Y, verse_end: Z, name: 'Pericope Name 2' },

  // Story B: [Story Title]
  { chapter: X, verse_start: Y, verse_end: Z, name: 'Pericope Name 3' },
];
```

**Naming convention:**
- Constant: `[BOOKNAME_CAPS]_PERICOPES`
  - Example: `KINGS_1_PERICOPES` (not `1KINGS_PERICOPES`)
  - Example: `SAMUEL_1_PERICOPES` (not `1SAMUEL_PERICOPES`)
- File: `[NN]_[bookname].js`
  - Example: `11_1kings.js` (not `1_1kings.js`)
  - Example: `09_1samuel.js`

---

## Part 5: Complete Workflow Example

### Input: Ruth Scene from Your Analysis

```markdown
### Scene A-1: Death in Moab

    Verse Range: 1:1-5

    Boundary Markers: (Start) Narrative opening: "In the days when the judges ruled, there was a famine..." (1:1). (End) Completion of tragedy: "both Mahlon and Chilion died, so that the woman was left without her two sons and her husband" (1:5).

    Literary Analysis: Verse 6 begins a new action ("Then she arose..."). This scene is the narrative setup, establishing the problem and the tragic descent in a structured downward spiral: famine → sojourn → death of Elimeleck → marriage of sons → death of sons. It ends with Naomi in complete emptiness.
```

### JSON Output

```json
{
  "scene_number": 1,
  "scene_name": "Death in Moab",
  "reference": "1:1-5",
  "why_start_end_and_devices": "Starts with narrative opening: 'In the days when the judges ruled, there was a famine...' (1:1). Ends with completion of tragedy: 'both Mahlon and Chilion died, so that the woman was left without her two sons and her husband' (1:5). Verse 6 begins a new action ('Then she arose...'). This scene is the narrative setup, establishing the problem and the tragic descent in a structured downward spiral: famine → sojourn → death of Elimeleck → marriage of sons → death of sons. It ends with Naomi in complete emptiness."
}
```

### First-Letter Pericope Output

```javascript
{ chapter: 1, verse_start: 1, verse_end: 5, name: 'Death in Moab' },
```

---

## Part 6: Continuation Tips for Seamless Workflow

### For Claude Sonnet (Codex)

When continuing with a different model and hitting context limits:

**Prompt template:**
```
I'm converting comprehensive literary analyses into JSON format for biblical books.
I've completed [BOOKS DONE]. Next, I need [BOOK NAME].

The conversion process:
1. Convert markdown literary analysis to JSON following the structure in /memory-method-bible/data/base-structure/[COMPLETED-BOOK]-base.json
2. Each book has:
   - Metadata: book_name, hebrew_name, canonical_grouping
   - big_picture_notes: Complete overview as single string
   - stories array with: story_letter, story_title, why_start_end_and_literary_glue, reference, scenes
   - scenes array with: scene_number (numeral only), scene_name, reference (chapter:verse-verse), why_start_end_and_devices

Here is my [BOOK NAME] literary analysis:

[PASTE YOUR MARKDOWN ANALYSIS]

Create the JSON file exactly as formatted in the completed examples.
```

### Key Continuity Points

1. **JSON structure is FIXED** - Don't ask for format variations; it must match existing files exactly
2. **Scene numbers are NUMERAL ONLY** - 1, 2, 3, not A-1, A-2, A-3
3. **All fields are SINGLE STRINGS** - No internal formatting; combine text into one flowing string
4. **References use CONSISTENT FORMAT** - "1:1 - 4:12" with spaces around dash
5. **No smart quotes** - Use straight quotes `"` not `"` or `"`

### Verification Before Handoff

Always run Node.js validation and confirm:
```
✅ [BOOK] JSON is VALID
Stories: [number]
Total scenes: [number]
[Story breakdown list]
```

---

## Part 7: Quick Reference Checklist

- [ ] Metadata extracted and properly formatted
- [ ] Big-picture notes combined into single string
- [ ] Each story has letter (A-Z), title, why_start_end_and_literary_glue, reference
- [ ] Each scene has scene_number (numeral), scene_name, reference, why_start_end_and_devices
- [ ] All internal quotes are straight quotes `"` not smart quotes
- [ ] All quotes in text content are escaped with backslash `\"`
- [ ] No trailing commas in arrays or objects
- [ ] Reference format is consistent: "chapter:verse - chapter:verse"
- [ ] Scene numbers are sequential within each story (1, 2, 3...)
- [ ] JSON validates with Node.js parser
- [ ] Total scene count is verified
- [ ] Committed with descriptive git message
- [ ] File follows naming convention: `[bookname]-base.json`

---

## Part 8: First-Letter Pericope Generation Script

**Quick conversion from JSON to pericopes:**

```javascript
// Convert existing JSON to pericope format
const fs = require('fs');

const bookData = JSON.parse(fs.readFileSync('data/base-structure/1kings-base.json', 'utf8'));
const pericopes = [];

bookData.stories.forEach(story => {
  story.scenes.forEach(scene => {
    const [chapterVerse, endVerse] = scene.reference.split('-');
    const [chapter, verseStart] = chapterVerse.split(':');

    pericopes.push({
      chapter: parseInt(chapter),
      verse_start: parseInt(verseStart),
      verse_end: parseInt(endVerse),
      name: scene.scene_name
    });
  });
});

console.log('export const KINGS_1_PERICOPES = [');
pericopes.forEach((p, i) => {
  console.log(`  { chapter: ${p.chapter}, verse_start: ${p.verse_start}, verse_end: ${p.verse_end}, name: '${p.name}' }${i < pericopes.length - 1 ? ',' : ''}`);
});
console.log('];');
```

---

## Summary

| Stage | Input | Output | Tool |
|-------|-------|--------|------|
| 1. Analysis | Literary markdown | Structured JSON | Manual conversion |
| 2. Validation | JSON file | Verification output | Node.js |
| 3. Version Control | JSON file | Commit hash | Git |
| 4. Pericope Creation | JSON file | JavaScript export | Manual/Script |

Each stage builds on the previous, creating a complete, reproducible pipeline for biblical literary analysis.
