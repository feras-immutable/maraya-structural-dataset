# Maraya Structural Dataset

_The Maraya Structural Dataset maps the compositional centers of all 114 surahs, enabling exploration of Qur'anic architecture through an open, reproducible framework._

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

---

## Overview

The Maraya Structural Dataset is a structured, JSON-based corpus documenting the compositional architecture of every surah in the Qur'an. Each entry is the product of a multi-pass analytical framework that identifies the structural pivot — the center of gravity — of a surah through the convergence of independent signals.

The dataset includes:

- **114 surah entries** with complete pivot analysis (verse, confidence, signal breakdown, axis type, offset)
- **Block maps** encoding the ring-composition or chiastic structure of each surah as labeled, role-tagged segments
- **Signal tables** recording per-verse signals (thematic shifts, lexical markers, mirror patterns, discourse moves, prosodic features)
- **Structure summaries** capturing the detected pattern, frame type, and block map per surah
- **Supporting data**: surah families, semantic profiles, metadata, and normative centrality classifications

---

## Quick Start

Each surah entry in `data/maraya_structural_dataset.json` contains a `pivot` object. Here is the Al-Fatiha (Surah 1) example:

```json
{
  "surah_number": 1,
  "surah_name_en": "Al-Fatiha",
  "verse_count": 7,
  "pivot": {
    "verse": 5,
    "verse_ar": "إِيَّاكَ نَعْبُدُ وَإِيَّاكَ نَسْتَعِينُ",
    "confidence": "high",
    "signal_count": 4,
    "signals": {
      "theme": true,
      "grammar": true,
      "prosody": true,
      "mirror": true
    },
    "notes": "Only unmirrored verse; doubled pronominal fronting unique in surah; shortest verse by syllable count; grammatical person pivot (3rd→2nd)",
    "axis_type": "geometric_center",
    "center_logic": "single_concentration",
    "offset": 0.2143
  }
}
```

Load all 114 surahs in Python:

```python
import json

with open("data/maraya_structural_dataset.json") as f:
    data = json.load(f)

for surah in data["surahs"]:
    print(surah["surah_number"], surah["surah_name_en"], surah["pivot"]["verse"])
```

---

## Files

| File | Description |
|------|-------------|
| `data/maraya_structural_dataset.json` | Primary dataset. 114 surah entries with pivot analysis, boundaries, signal tables, and structure summaries. |
| `data/blockMap.json` | Block-level ring/chiastic maps for all 114 surahs. Each surah is a labeled sequence of role-tagged blocks with verse ranges. |
| `data/surah_metadata.json` | Per-surah metadata: Arabic and English names, name meaning, revelation phase (Meccan/Medinan), revelation order, and juz range. |
| `data/surah_families.json` | Typological family classification for all 114 surahs across 7 family types, with pivot function and center logic fields. |
| `data/semantic_profiles.json` | Normalized semantic density scores (early, pivot, late sections) and pivot advantage per surah. |
| `data/normative_centrality/classifications_claude.json` | Claude-generated pivot and control verse category classifications for all 114 surahs. |
| `data/normative_centrality/classifications_gpt4.txt` | GPT-4-generated pivot and control verse category classifications (JSON lines). |
| `data/normative_centrality/pivot_classification_input.json` | Input records used for both model classification runs: pivot and control verse text with metadata. |

---

## Schema

See [schema.md](schema.md) for complete field documentation.

---

## Methodology

Each pivot was identified through a **six-pass convergence framework** applied independently across five analytical dimensions:

1. **Theme** — thematic shift or concentration
2. **Lexical** — inclusio, concatenation, root repetition
3. **Mirror** — ring/chiastic correspondence
4. **Discourse** — person, mode, or register shift
5. **Prosody** — rhythm, rhyme class, syllabic weight

A pivot is assigned `high` confidence when 4 or more independent signals converge at a single verse, `medium` when 2–3 signals converge within a 2-verse window, and `low` when a single unconfirmed signal is present.

See [methodology/six-pass-framework.md](methodology/six-pass-framework.md) for the full protocol.

---

## Citation

```bibtex
@dataset{mansi2026maraya,
  author    = {Mansi, Feras},
  title     = {Maraya Structural Dataset},
  year      = {2026},
  publisher = {Ayah Labs},
  version   = {1.0.0},
  url       = {https://github.com/ayahlabs/maraya-structural-dataset},
  license   = {CC-BY-4.0}
}
```

See [CITATION.cff](CITATION.cff) for machine-readable format.

---

## Links

- **Maraya**: [PLACEHOLDER_URL]
- **Ayah Labs**: [https://ayahlabs.com](https://ayahlabs.com)
- **Zenodo**: [PLACEHOLDER_DOI]

---

## License

This dataset is released under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

You are free to share and adapt the material for any purpose, provided appropriate credit is given.
