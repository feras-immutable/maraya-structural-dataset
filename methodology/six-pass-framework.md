# Six-Pass Structural Analysis

_A methodology for detecting ring composition in Qur'anic surah architecture._

Ayah Labs | Methodology Document v1.0 | March 2026

---

## 1. Overview

The Six-Pass Structural Analysis is a systematic methodology for detecting, verifying, and characterizing ring composition (chiastic structure) in Qur'anic surahs. It applies five independent signal-detection passes plus a convergence synthesis to each surah, producing a structural profile that includes: the pivot location, signal count, center-offset, detected pattern, and cross-surah connections.

The methodology was developed through the iterative analysis of all 114 surahs of the Qur'an (6,236 verses) and validated against two non-Qur'anic control texts: the Sermon on the Mount (Matthew 5-7) and the Genesis Flood Narrative (Genesis 6:9-9:17).

**Core principle:** A structural center is confirmed only when multiple independent signals converge at the same location. No single pass is sufficient; convergence is the criterion.

Ring composition produces a nested mirror structure around a central pivot:

```
  A   ───────────────────────────  A'
    B  ────────────────────────  B'
      C  ──────────────────  C'
             X (pivot)
```

Each outer pair (A/A', B/B', C/C') shares thematic, lexical, or structural correspondence. The pivot (X) sits at the center.

---

## 2. AI Assistance Transparency

This analysis was conducted with the assistance of Claude (Anthropic). The AI was used as a research tool for: systematic signal detection across all passes, consistency checking across 114 surahs, and documentation of findings. All analytical judgments (pivot identification, signal assessment, pattern classification) were made through iterative human-AI collaboration, with the human analyst directing the investigation and validating outputs against primary Arabic text and prior scholarship.

---

## 3. The Six Passes

Each surah is analyzed through six sequential passes. Passes 1-5 each detect a distinct type of structural signal. Pass 6 is not a new signal but a convergence synthesis of the five independent detection passes.

### Pass 1: Thematic Shift Detection + Block Map

**Objective:** Identify thematic blocks and determine whether the surah's discourse follows a linear (progressive) or ring (mirrored) trajectory.

**Method:** Read the surah sequentially, marking every point where the primary theme, topic, or narrative focus shifts. Assign each contiguous block a label (A, B, C... D ... C', B', A') and a verse range. Identify the candidate structural center (D).

**Output:** A block map table (ID / Verses / Count / Label / Role) with compressed descriptions. Each block's role is classified as: `outer_frame_open`, `inner_frame_open`, `center_flank_left`, `center`, `center_flank_right`, `inner_frame_close`, `outer_frame_close`.

**Center-offset calculation:**

- Geometric center = (verse_count + 1) / 2
- Pivot center = (first_pivot_verse + last_pivot_verse) / 2
- Offset = (pivot_center - geometric_center) / verse_count
- Values near zero indicate precise centering

### Pass 2: Lexical Repetition / Framing Detection

**Objective:** Detect lexical inclusios (framing devices where the same word, phrase, or formula appears at the surah's opening and closing) and internal keyword-chains that reinforce the ring structure.

**Method:** Compare the surah's first and last blocks for shared vocabulary, divine-name pairs, or formulaic expressions. Then trace key terms across the entire surah to identify threading patterns and concentrated deployments at the pivot.

**Output:** An inclusio table (Pair / Verse A / Verse B / Type / Notes) and a key-concatenations table documenting significant lexical deployments. Each inclusio is classified as: `exact` (identical wording), `near` (same root/concept), or `thematic` (same domain but different vocabulary).

### Pass 3: Mirrored Thematic Structure

**Objective:** Verify whether the thematic blocks identified in Pass 1 mirror around the candidate center, forming a ring (A-B-C-D-C'-B'-A') rather than a linear sequence.

**Method:** For each outer block-pair (A/A', B/B', C/C'), assess whether they share: (a) the same thematic domain, (b) complementary or reversed content, (c) shared vocabulary, (d) structural parallelism. Each pair receives a quality rating: `EXACT`, `STRONG`, `MODERATE`, `WEAK`, or `NO MATCH`.

**Output:** A ring diagram (ASCII representation of the nested structure), a mirror-correspondences table explaining each pair, and a `detected_pattern` classification: `ring_composition` (with block count), `linear`, `refrain_governed`, or `hybrid`.

### Pass 4: Discourse / Addressee Shift Analysis

**Objective:** Assess whether the candidate pivot exhibits concentrated discourse-mode convergence, the hallmark of Qur'anic structural centers.

**Method:** At the candidate pivot, count the number of distinct discourse modes present: legislation, declaration, rhetorical question, command/prohibition, prayer, eschatological scene, historical narrative, addressee shift, parable, conditional, and principle-statement. Also note any key discourse observations (unique verses, foundational declarations, unprecedented formulations).

**Output:** A count of discourse modes at the pivot (Qur'anic pivots typically show 8-12 modes in 9-14 verses) and a numbered list of key discourse observations with analytical commentary.

### Pass 5: Prosodic / Rhyme (Saj') Analysis

**Objective:** Detect whether the surah's end-rhyme (saj'/fasilah) patterns reinforce the structural center through zone-shifts, convergence, or unique terminals at the pivot.

**Method:** Identify the governing rhyme family (e.g., nasal-final [-un/-in/-im]) and its dominance percentage. Note the opening terminal, closing terminal, and pivot-center terminal. Identify any unique or rare rhyme-terminals that appear exclusively at the pivot. Assess whether rhyme-family shifts correspond to thematic block boundaries.

**Output:** A zone analysis describing the rhyme arc (opening to closing), the pivot terminal, and the governing sound family. A mandatory `signal_table` is produced for surahs where prosodic data is particularly rich.

### Pass 6: Additional Structural Indicators + Signal Convergence

**Objective:** Synthesize all five signals into a convergence assessment and flag any additional structural indicators unique to this surah.

**Method:** Construct a Signal Convergence Table with five rows (Theme / Lexical / Mirror / Discourse / Rhyme), each assessed at the candidate pivot. Each signal is marked as present or absent with a content description. The total signal count (out of 5) determines confidence. Additionally, list additional structural indicators: unprecedented verses, unique structural features, record-setting metrics.

**Output:** Signal Convergence Table, structural indicators, cross-surah flags (connecting this surah's findings to other surahs), a Structure Summary table, and a Pivot Survey Entry.

---

## 4. Confidence Criteria

The confidence rating is determined by signal convergence at the candidate pivot:

| Score | Signals Confirmed | Assessment |
|-------|-------------------|------------|
| 5/5 (high) | All five signals converge | Strong ring composition confirmed |
| 4/5 | Four signals; one absent or weak | Ring composition probable |
| 3/5 | Three signals | Partial ring or hybrid structure |
| 2/5 or below | Two or fewer | Ring composition not confirmed |

Across the 114-surah corpus, each identified pivot location satisfies the convergence criteria, with multiple independent signals aligning at a single structural point.

---

## 5. Center Logic Classifications

The `center_logic` field classifies how the pivot operates within the ring structure:

| Type | Definition | Example |
|------|-----------|---------|
| `compound_seam` | Multiple thematic threads converge in a multi-verse block at the center | Q.2:142-152 |
| `single_concentration` | One dominant theme/verse functions as the axis | Q.1:5 |
| `terminal` | The pivot sits at or near the surah's end rather than its geometric center | Some short surahs |
| `refrain_governed` | A repeated refrain structures the surah, with the center marked by a refrain variation | Q.55 |
| `geometric_center` | The center is identified primarily by position rather than thematic weight | Rare |
| `kalla_pillar` | The word "kalla" functions as a structural marker dividing the surah | Q.83 |

---

## 6. Control Validation

The methodology was validated against two non-Qur'anic control texts to test its discriminatory power:

**Control 1: Sermon on the Mount (Matthew 5-7)**
Result: 1-2/5 signal convergence. The text is structurally linear (progressive teaching), not ring. The methodology correctly identifies the absence of ring composition.

**Control 2: Genesis Flood Narrative (Genesis 6:9-9:17)**
Result: 3/5 signal convergence. Ring composition IS detected (confirmed by Wenham 1978). Theme, lexical mirroring, and mirror structure all confirmed. However: no discourse convergence at center and no prosodic signal (Hebrew prose lacks saj'). The methodology correctly detects ring composition where it exists AND correctly identifies the two signal layers unique to the Qur'an.

| Metric | Qur'an (114 surahs) | Genesis Flood | Sermon on Mount |
|--------|---------------------|---------------|-----------------|
| Ring composition | Detected in all 114 | Yes | No |
| Lexical framing | Detected in all 114 | Yes | No |
| Mirror structure | Detected in all 114 | Yes | No |
| Discourse convergence | Detected in all 114 | No (1 mode) | No |
| Prosodic signal | Detected in all 114 | No (prose) | No |
| Signal convergence | High (4-5/5) | 3/5 | 1-2/5 |

---

## 7. Citation

This methodology draws on and extends the structural analysis traditions of:

- **Raymond Farrin**: Ring composition analysis of Q.2 Al-Baqarah (*Structure and Qur'anic Interpretation*, 2014)
- **Neal Robinson**: Numerical centering and structural analysis (*Discovering the Qur'an*, 2003)
- **Heba El-Tahry**: Keyword and inclusio analysis (*Exploring the Qur'an's Ring Structure*)
- **Michel Cuypers**: Rhetorical analysis and Semitic ring composition (*The Composition of the Qur'an*, 2015)
- **Gordon Wenham**: Chiastic analysis of the Genesis Flood Narrative (1978) -- used as control

The six-pass methodology synthesizes these traditions into a reproducible, multi-signal framework and extends it to the complete 114-surah corpus for the first time.

---

## Links

- **Dataset:** [github.com/ayahlabs/maraya-structural-dataset](https://github.com/ayahlabs/maraya-structural-dataset)
- **Maraya** (interactive viewer): PLACEHOLDER_URL
- **Ayah Labs:** [ayahlabs.com](https://ayahlabs.com)
