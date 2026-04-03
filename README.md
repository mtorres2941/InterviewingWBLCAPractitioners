# Interviewing wbLCA Practitioners

Analysis of a survey study on whole-building life cycle assessment (wbLCA) practitioners — examining demographics, tool usage, time allocation, team size, and participation in commitment programs (SE2050, AIA 2030). Developed as part of a PhD dissertation at CU Boulder.

## Repository Structure

```
InterviewingWBLCAPractitioners/
├── SurveyWBLCAPractitioners.ipynb   # Main analysis notebook
├── data/
│   └── raw/
│       ├── SurveyStudyAnalysis.xlsx  # Survey data (sheets: SE2050, A2030, SurveyResults, Tagging)
│       └── CategorizingTags.xlsx     # Manual tag categorization reference
├── outputs/
│   ├── figures/                      # 14 demographic and survey result figures (PNG)
│   └── tables/
│       └── tagcounts.xlsx            # Tag frequency counts
├── .gitignore
├── README.md
└── environment.yml
```

## Setup

```bash
conda env create -f environment.yml
conda activate interviewing_wblca
jupyter lab
```

## Author

Martin Torres — CU Boulder, PhD Candidate
GitHub: [mtorres2941](https://github.com/mtorres2941)
