# Schema Reference

Field-by-field documentation for all data files in the Maraya Structural Dataset.

---

## 1. `data/maraya_structural_dataset.json`

**Purpose:** Primary dataset. Contains the complete pivot analysis for all 114 surahs.

**Top-level structure:** Object with metadata fields and a `surahs` array.

### Top-level fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `schema_version` | string | Semantic version of the dataset schema | `"1.0.0"` |
| `methodology` | string | Short description of the analytical method | `"Multi-pass structural convergence analysis"` |
| `passes` | array of strings | Ordered list of analytical passes applied | `["theme", "lexical", "mirror", "discourse", "prosody"]` |
| `confidence_rubric` | object | Definitions for each confidence level (see below) | — |
| `surahs` | array of objects | One entry per surah, ordered 1–114 | — |

### `confidence_rubric` fields

| Field | Type | Description |
|-------|------|-------------|
| `high` | string | Definition of high confidence | `"4+ independent signals converge at single verse"` |
| `medium` | string | Definition of medium confidence | `"2–3 signals converge within 2-verse window"` |
| `low` | string | Definition of low confidence | `"1 signal, unconfirmed by secondary pass"` |

### Per-surah fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `surah_number` | integer | Canonical surah number (1–114) | `1` |
| `surah_name_ar` | string | Arabic name of the surah | `"الفاتحة"` |
| `surah_name_en` | string | Transliterated English name | `"Al-Fatiha"` |
| `verse_count` | integer | Total number of verses in the surah | `7` |
| `pivot` | object | Structural pivot analysis (see below) | — |
| `boundaries` | array of objects | Labeled structural boundary segments (see below) | — |
| `signal_table` | array of objects | Per-verse signal records (see below) | — |
| `structure_summary` | object | High-level structural pattern summary (see below) | — |
| `verses` | array of objects | Arabic verse texts; each has `n` (integer) and `ar` (string) | — |

### `pivot` object fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `verse` | integer | Verse number of the identified pivot | `5` |
| `verse_ar` | string | Arabic text of the pivot verse | `"إِيَّاكَ نَعْبُدُ وَإِيَّاكَ نَسْتَعِينُ"` |
| `confidence` | string | Confidence level: `"high"`, `"medium"`, or `"low"` | `"high"` |
| `signal_count` | integer | Number of independent signals confirming this pivot | `4` |
| `signals` | object | Boolean flags per signal type (keys vary by surah; common keys: `theme`, `grammar`, `prosody`, `mirror`, `lexical`, `discourse`) | `{"theme": true, "grammar": true, "prosody": true, "mirror": true}` |
| `notes` | string | Analytical notes explaining the pivot identification | `"Only unmirrored verse; doubled pronominal fronting..."` |
| `axis_type` | string | Classification of the axis geometry (e.g., `"geometric_center"`, `"compound_seam"`, `"distributed_zone"`) | `"geometric_center"` |
| `center_logic` | string | Logic type for center determination (e.g., `"single_concentration"`, `"compound_seam"`) | `"single_concentration"` |
| `center_logic_note` | string | Extended note on center logic reasoning | `"geometric center v.5 (4/5)..."` |
| `signal_count_confirmed` | integer | Final confirmed signal count after review | `4` |
| `offset` | number | Fractional offset of the pivot from the geometric center of the surah (0 = exact center) | `0.2143` |

### `boundaries` array — per-item fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `label` | string | Human-readable name for this boundary segment | `"Frame A"` |
| `verses` | array of 2 integers | Start and end verse numbers (inclusive) | `[1, 3]` |
| `signal_count` | integer | Number of signals supporting this boundary | `3` |
| `signals` | array of strings | Signal type labels for this boundary | `["lexical_inclusio", "mirror_open", "prosodic_anchor"]` |
| `notes` | string | Analytical notes for the boundary | `"الرَّحْمٰنِ الرَّحِيمِ — exact repetition vv. 1 & 3"` |

### `signal_table` array — per-item fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `verse` | integer | Verse number | `1` |
| `verse_ar` | string | Arabic text of the verse | `"بِسْمِ اللهِ الرَّحْمٰنِ الرَّحِيمِ"` |
| `theme_shift` | boolean | Whether a thematic shift occurs at this verse | `false` |
| `theme_detail` | string \| null | Description of the thematic shift (present when `theme_shift` is true) | `"3rd-person characterization → 1st-person petition"` |
| `lexical_signal` | string \| null | Lexical signal type (e.g., `"inclusio_open"`, `"inclusio_close"`, `"concatenation_open"`, `"concatenation_close"`) or null | `"inclusio_open"` |
| `lexical_detail` | string \| null | Detail note for the lexical signal | `"الرَّحْمٰنِ الرَّحِيمِ — frame opens"` |
| `mirror_signal` | string \| null | Mirror/ring signal label (e.g., `"frame_A_open"`, `"unmirrored_center"`, `"frame_B_close"`) | `"frame_A_open"` |
| `discourse_shift` | boolean | Whether a discourse shift (person, mode, or register) occurs | `false` |
| `discourse_detail` | string \| null | Description of the discourse shift | `"huwa/absent (3rd) → anta/present (2nd)"` |
| `rhyme_class` | string \| null | IPA-style rhyme class label | `"-iːm"` |
| `prosody_note` | string \| null | Prosodic observation for the verse | `"anchor vowel established"` |

### `structure_summary` object fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `detected_pattern` | string | Structural pattern label (e.g., `"ring_composition_candidate"`) | `"ring_composition_candidate"` |
| `axis_type` | string | Axis type (e.g., `"single_verse_pivot"`, `"multi_verse_zone"`) | `"single_verse_pivot"` |
| `frame_type` | string | Frame type shorthand (e.g., `"ABA_prime"`, `"ABCBA"`) | `"ABA_prime"` |
| `block_map` | object | Keyed block map (keys: `A`, `B`, `X`, `B_prime`, `A_prime`, etc.); each value has `verses` (array of 2 integers) and `label` (string) | — |

---

## 2. `data/blockMap.json`

**Purpose:** Ring-composition or chiastic block maps for all 114 surahs, encoded as labeled, role-tagged segments with verse ranges.

**Top-level structure:** Object keyed by surah number as a string (`"1"` through `"114"`). Each value is an array of block objects.

### Per-block fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `id` | string | Block identifier within the surah (e.g., `"A"`, `"B"`, `"PIVOT"`, `"C₀"`, `"A′"`) | `"PIVOT"` |
| `v` | array of 2 integers | Verse range: `[start, end]` (inclusive) | `[5, 5]` |
| `role` | string | Structural role of the block (see role values below) | `"pivot"` |
| `label` | string | Human-readable description of the block's content | `"Worship and reliance"` |

### Possible `role` values

| Value | Description |
|-------|-------------|
| `pivot` | The structural pivot block |
| `frame` | General frame segment (opening or closing) |
| `outer_frame_open` | Outer frame, opening side |
| `outer_frame_close` | Outer frame, closing side |
| `inner_frame_open` | Inner frame, opening side |
| `inner_frame_close` | Inner frame, closing side |
| `body` | Main body segment |
| `center` | Center segment (used in some symmetric structures) |
| `center_flank_left` | Segment immediately left/before the center |
| `center_flank_right` | Segment immediately right/after the center |
| `hinge` | Hinge or turning-point segment |
| `seam` | Seam between two major sections |
| `close` | Closing segment |
| `addendum` | Appended segment outside the primary structure |
| `narrative_1` … `narrative_7` | Numbered narrative segments (for surahs with sequential narrative blocks) |
| `transition_1` … `transition_3` | Numbered transition segments |

---

## 3. `data/surah_families.json`

**Purpose:** Typological family classification for all 114 surahs. Groups surahs by compositional form and semantic character.

**Top-level structure:** Array of 114 objects, one per surah, ordered by surah number.

### Per-surah fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `surah_number` | integer | Canonical surah number (1–114) | `1` |
| `surah_name` | string | Transliterated English name | `"Al-Fatiha"` |
| `family_id` | integer | Numeric identifier for the family (1–7) | `3` |
| `family_name` | string | Human-readable family name (see family types below) | `"Compressed crystal"` |
| `family_description` | string | One-line description of the family | `"A tightly woven surah — one idea, one center"` |
| `pivot_function` | string | Semantic function of the pivot verse (see values below) | `"THEOLOGICAL_DECLARATION"` |
| `center_logic` | string | Center logic type (matches `pivot.center_logic` in primary dataset) | `"single_concentration"` |
| `form` | string | Formal distribution type: `"compressed"` or `"distributed"` | `"compressed"` |
| `semantic` | string | Semantic density character: `"concentrated"`, `"diffuse"`, or `"transitional"` | `"concentrated"` |

### Family types

| `family_id` | `family_name` | Description |
|------------|---------------|-------------|
| 1 | Narrative pillar | Long narrative surah turning through story |
| 2 | Communal address | Surah primarily addressed to the believing community |
| 3 | Compressed crystal | Tightly woven surah — one idea, one center |
| 4 | Polemical hinge | Surah turning through argument and address |
| 5 | Distributed field | Surah unfolding across a wide landscape |
| 6 | Compact proclamation | Short to mid-length surah with concentrated proclamation |
| 7 | Singular architecture | Unique structural form not fitting other families |

### `pivot_function` values

| Value | Description |
|-------|-------------|
| `THEOLOGICAL_DECLARATION` | Pivot declares divine attributes or fundamental theological realities |
| `COMMAND_LEGISLATION` | Pivot issues directives, commands, or legislative prescriptions |
| `COMMUNAL_ADDRESS` | Pivot directly addresses the believing community |
| `NARRATIVE_RECOLLECTION` | Pivot recounts a prophetic or historical episode |
| `WARNING_CONSEQUENCE` | Pivot warns of judgment, punishment, or consequences |
| `POLEMIC_APOLOGETIC` | Pivot refutes opponents or defends revelation |

---

## 4. `data/semantic_profiles.json`

**Purpose:** Normalized semantic density scores for each surah's three structural zones (early, pivot, late), used to characterize where semantic weight is concentrated.

**Top-level structure:** Object keyed by surah number as a string (`"1"` through `"114"`). Each value is a profile object.

### Per-surah fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `early` | number | Normalized semantic density score for the early section of the surah (0.0–1.0) | `0.667` |
| `pivot` | number | Normalized semantic density score at the pivot zone (0.0–1.0) | `1.0` |
| `late` | number | Normalized semantic density score for the late section (0.0–1.0) | `0.8` |
| `pivot_advantage` | number | Difference between the pivot score and the average of early and late scores; positive values indicate pivot-concentrated surahs | `0.3333` |
| `type` | string | Distribution type: `"compressed"` or `"distributed"` | `"compressed"` |

---

## 5. `data/surah_metadata.json`

**Purpose:** Standard bibliographic and revelatory metadata for all 114 surahs.

**Top-level structure:** Array of 114 objects, one per surah, ordered by surah number.

### Per-surah fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `surah_number` | integer | Canonical surah number (1–114) | `1` |
| `name_en` | string | Transliterated English name | `"Al-Fatiha"` |
| `name_ar` | string | Arabic name | `"الفاتحة"` |
| `name_meaning` | string | English translation of the surah name | `"The Opening"` |
| `phase` | string | Revelation phase: `"Meccan"` or `"Medinan"` | `"Meccan"` |
| `revelation_order` | integer | Traditional order of revelation (1–114) | `5` |
| `juz` | string | Juz range as a display string (e.g., `"1"` or `"1–3"`) | `"1"` |
| `juz_start` | integer | First juz containing this surah | `1` |
| `juz_end` | integer | Last juz containing this surah | `1` |
| `exceptions` | string \| null | Notable exceptions to the phase classification (specific verses with different provenance), or null | `"v.281 revealed at Mina on Farewell Pilgrimage"` |
| `has_exceptions` | boolean | Whether any verse-level phase exceptions exist | `false` |

---

## 6. `data/normative_centrality/`

This directory contains three files supporting the normative centrality experiment: independent LLM classification of pivot and control verses to test whether model-identified categories align with structurally derived pivots.

---

### `pivot_classification_input.json`

**Purpose:** Input records provided to both LLM classifiers. Contains the pivot and control verses (with translations) for each surah, drawn from the primary dataset.

**Top-level structure:** Array of 114 objects.

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `surah_number` | integer | Surah number | `1` |
| `surah_name_en` | string | Transliterated English name | `"Al-Fatiha"` |
| `surah_name_ar` | string | Arabic name | `"الفاتحة"` |
| `verse_count` | integer | Total verses in the surah | `7` |
| `center_logic` | string | Center logic type from primary dataset | `"single_concentration"` |
| `offset` | number | Pivot offset from geometric center | `0.2143` |
| `pivot_start` | integer | First verse of the pivot block | `5` |
| `pivot_end` | integer | Last verse of the pivot block | `5` |
| `pivot_verse_count` | integer | Number of verses in the pivot block | `1` |
| `pivot_block_id` | string | Block ID of the pivot in the block map | `"PIVOT"` |
| `pivot_block_role` | string | Role of the pivot block | `"pivot"` |
| `pivot_block_label` | string | Label of the pivot block | `"Worship and reliance"` |
| `pivot_verses` | array of objects | Pivot verse records; each has `n` (integer), `ar` (string), `en` (string) | — |
| `control_start` | integer | First verse of the control block | `1` |
| `control_end` | integer | Last verse of the control block | `1` |
| `control_verses` | array of objects | Control verse records; each has `n` (integer), `ar` (string), `en` (string) | — |

---

### `classifications_claude.json`

**Purpose:** Claude-generated classifications of pivot and control verses for all 114 surahs. Each record captures the predicted category and confidence for both the pivot and the control passage.

**Top-level structure:** Array of 114 objects.

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `surah_number` | integer | Surah number | `1` |
| `pivot_category` | string | Predicted category for the pivot verse (see category values) | `"THEOLOGICAL_DECLARATION"` |
| `pivot_confidence` | string | Model confidence: `"high"` or `"medium"` | `"high"` |
| `pivot_reasoning` | string | Model's reasoning for the pivot classification | `"Declares exclusive worship and reliance upon Allah..."` |
| `pivot_secondary_candidate` | string \| null | Secondary category candidate if confidence was split, else null | `null` |
| `control_category` | string | Predicted category for the control verse | `"THEOLOGICAL_DECLARATION"` |
| `control_confidence` | string | Model confidence for the control classification | `"high"` |
| `control_reasoning` | string | Model's reasoning for the control classification | `"Opens with invocation of Allah's names..."` |
| `control_secondary_candidate` | string \| null | Secondary candidate for control classification, or null | `null` |

---

### `classifications_gpt4.txt`

**Purpose:** GPT-4-generated classifications of the same pivot and control verses. Stored as a JSON array in a `.txt` file. Structure is identical to `classifications_claude.json`.

**Top-level structure:** JSON array of 114 objects with the same fields as `classifications_claude.json`.

---

### Category values (used in both classification files)

| Value | Description |
|-------|-------------|
| `THEOLOGICAL_DECLARATION` | Asserts divine attributes, sovereignty, or unseen theological realities |
| `COMMAND_LEGISLATION` | Issues directives, prohibitions, or prescribed conduct |
| `COMMUNAL_ADDRESS` | Addresses believers in a pastoral or identity-forming way |
| `NARRATIVE_RECOLLECTION` | Recounts a prophetic or historical episode |
| `WARNING_CONSEQUENCE` | Focuses on judgment, punishment, or consequences of disbelief |
| `POLEMIC_APOLOGETIC` | Refutes opponents or defends revelation through argument |
