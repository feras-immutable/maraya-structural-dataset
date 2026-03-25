# Maraya Structural Dataset

_The Maraya Structural Dataset maps the compositional centers of all 114 surahs of the Qur'an, enabling exploration of Qur'anic architecture through an open, reproducible framework._

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

---

## Overview

The Maraya Structural Dataset is a structured, JSON-based corpus documenting the compositional architecture of every surah in the Qur'an. Each entry is the product of a multi-pass analytical framework that identifies the structural pivot — the center of gravity — of a surah through the convergence of independent signals.

The dataset includes:

- **114 surah entries** with complete pivot analysis (verse, confidence, signal breakdown, axis type, offset)
- **Block maps** encoding the ring-composition or chiastic structure of each surah as labeled, role-tagged segments
- **Signal tables** recording per-verse signals (thematic shifts, lexical markers, mirror patterns, discourse moves, prosodic features)
- **Structure summaries** capturing the detected pattern, frame type, and block map per surah

---

## Why this dataset exists

The Qur'an has long been studied for compositional structure, including ring composition, chiastic symmetry, and thematic centering. However, no corpus-wide dataset documenting structural pivots across all 114 surahs previously existed. The Maraya Structural Dataset provides a unified, reproducible registry enabling comparative analysis, visualization, and further research.

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
    "confidence": "high",
    "signal_count": 4,
    "signals": { "theme": true, "grammar": true, "prosody": true, "mirror": true },
    "axis_type": "geometric_center",
    "offset": 0.2143
  }
}
```

The block map shows how Al-Fatiha's 7 verses form a ring around the pivot:

```
  A  | 1-3  | Praise of the Lord
  B  | 4    | Lord of Judgment
  X  | 5    | Pivot: Worship and reliance
  B' | 6    | Prayer for guidance
  A' | 7    | The three paths
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

---

## Use cases

- Structural Qur'an readers and visualizations
- Hifz (memorization) structure aids
- Structural tafsir research
- Academic comparative analysis
- Plugin and tool development
- Cross-surah pattern exploration

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

A pivot is assigned `high` confidence when 4 or more independent signals converge at a single verse, `medium` when 2-3 signals converge within a 2-verse window, and `low` when a single unconfirmed signal is present.

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
  url       = {https://github.com/feras-immutable/maraya-structural-dataset},
  license   = {CC-BY-4.0}
}
```

See [CITATION.cff](CITATION.cff) for machine-readable format.

---

## Links

- **Maraya**: https://maraya.app
- **Ayah Labs**: [ayahlabs.com](https://ayahlabs.com)
- **Zenodo**: https://doi.org/10.5281/zenodo.19224437

---

## License

This dataset is released under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

You are free to share and adapt the material for any purpose, provided appropriate credit is given.
