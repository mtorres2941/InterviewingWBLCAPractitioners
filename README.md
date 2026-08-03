# Interviewing wbLCA Practitioners

Analysis code and de-identified data for a semi-structured interview study of
whole-building life cycle assessment (wbLCA) practitioners (n = 46), practising
primarily in the United States with a small number based in Canada. The study
examines practitioner demographics, tool usage,
time allocation, team structure, data sources, problems encountered in practice,
and receptiveness to advanced LCA methods (parametric and dynamic LCA).

Developed as part of a PhD dissertation in Architectural Engineering at the
University of Colorado Boulder, in Dr. Wil Srubar's Living Materials Laboratory.

<!-- TODO: add Zenodo DOI badge once the deposit is created -->

## Study design

Forty-six practitioners were recruited from three sampling frames: signatories of
the SE 2050 commitment program, signatories of AIA 2030, and practitioners at
firms belonging to neither ("NonCP"). Participants are architects (20), engineers
(20), and sustainability consultants (6).

Interviews were semi-structured. Responses were coded inductively: an initial
coding pass (TAG1) was consolidated into a final code set (TAG2) via the mapping
recorded in the `Retagging` sheet. **All counts in the analysis are counts of
participants who volunteered a topic, not responses to closed-ended items.** A
participant who did not mention a topic was not necessarily asked about it, so
every count should be read as a lower bound on prevalence rather than a response
rate.

## Data availability and de-identification

The interview data in this repository has been de-identified. Specifically, the
following were removed or generalized before publication:

| Field | Action | Reason |
|---|---|---|
| `Tagging.NOTE` | removed | Raw interview notes containing named employers, cities, universities, and gendered pronouns for 37 of 46 participants |
| `Tagging.TAG1` | removed | Pre-retagging codes; one entry named a participant's employer |
| `SurveyResults.Interview Date` | removed | Quasi-identifier in combination with firm and role |
| One `TOOL:` code | generalized to `in-house carbon calculator` | The code named the employer that developed the tool |

None of these fields are used by the analysis; every figure and table in the
notebook reproduces identically without them. Interviews were conducted between
2025-06-20 and 2026-01-06.

The identifiable source data is not distributed and is retained by the author
under the study's IRB protocol. <!-- TODO: add IRB protocol number -->

Firm-level attributes in the `SE2050`, `A2030`, and `NonCP` sampling-frame sheets
are pre-binned (e.g. employee counts as `D: 201-500`) and contain no firm names.

## Repository structure

```
InterviewingWBLCAPractitioners/
├── SurveyWBLCAPractitioners.ipynb   # Main analysis notebook
├── data/
│   └── raw/
│       ├── SurveyStudyAnalysis.xlsx  # De-identified study data (7 sheets)
│       └── CategorizingTags.xlsx     # Manual tag categorization reference
├── outputs/
│   ├── figures/                      # 19 figures (PNG)
│   └── tables/
│       ├── tagcounts.xlsx            # Tag frequency counts
│       └── top_comments_by_category.xlsx  # Codes cited by >=20% of participants
├── CITATION.cff
├── LICENSE                           # MIT (code)
├── LICENSE-DATA                      # CC BY 4.0 (data)
├── environment.yml
└── README.md
```

## Data dictionary

### `data/raw/SurveyStudyAnalysis.xlsx`

| Sheet | Rows | Description |
|---|---|---|
| `SE2050` | 138 | SE 2050 sampling frame: firm size, involvement, binned employee count, ECAP count |
| `A2030` | 651 | AIA 2030 sampling frame: firm size, involvement, binned employee count, projects reported |
| `NonCP` | 8 | Non-commitment-program sampling frame |
| `SurveyResults` | 46 | One row per participant: discipline, education, role, firm size, licensure, sustainability certifications, involvement |
| `Tagging` | 3504 | One row per coded utterance: participant `ID`, `CATEGORY`, final code `TAG2` |
| `Retagging` | 1025 | TAG1 → TAG2 consolidation mapping |
| `Categorizing Tags` | 578 | Manual assignment of codes to thematic categories |

Key columns in `Tagging`:

- **`ID`** — participant identifier (`I01`–`I46`), matching `SurveyResults.ID`
- **`TAG2`** — the final code, formatted `CATEGORY: statement (specific value)`
- **`CATEGORY`** — derived from the `TAG2` prefix at load time (see below)
- **`CATEGORY.1`** — coarse thematic grouping (e.g. `Traditional LCA: Problems`)

Analysis conventions applied when the data is loaded:

1. Rows where retagging discarded the code (`TAG2 == 'N/A:'`) are dropped.
2. Repeat codes within a single interview are de-duplicated, so each
   `(ID, TAG2)` pair appears once and a code's frequency equals its participant
   count.
3. `CATEGORY` is re-derived from the `TAG2` prefix. The stored `CATEGORY` values
   were written against TAG1 and are stale — 212 rows disagreed with their own
   `TAG2` prefix, and the category `RESOURCES` no longer exists in TAG2 (it was
   folded into `LEARNING:`). The original is preserved as `CATEGORY_TAG1`.

## Reproducing the analysis

```bash
conda env create -f environment.yml
conda activate interviewing_wblca
jupyter lab
```

Then run all cells in `SurveyWBLCAPractitioners.ipynb`. The notebook writes all
figures to `outputs/figures/` and all tables to `outputs/tables/`. It reads only
from `data/raw/` and is safe to re-run from a clean checkout.

To execute headlessly:

```bash
jupyter nbconvert --to notebook --execute --inplace SurveyWBLCAPractitioners.ipynb
```

## Citation

If you use this data or code, please cite it via the metadata in
`CITATION.cff`, or the Zenodo DOI once minted.

## License

- **Code** (`SurveyWBLCAPractitioners.ipynb`): MIT — see [LICENSE](LICENSE)
- **Data** (`data/`, `outputs/`): CC BY 4.0 — see [LICENSE-DATA](LICENSE-DATA)

## Author

Martín Torres — PhD Candidate, Architectural Engineering, University of Colorado Boulder
GitHub: [mtorres2941](https://github.com/mtorres2941)
