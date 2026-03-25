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

