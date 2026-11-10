# Devpost Hackathons Analysis

A data cleaning and exploratory analysis of 10,000+ hackathons listed on Devpost (2009-2024).

## Dataset

- **Source:** [Kaggle: aceeedev/hackathons](https://www.kaggle.com/datasets/aceeedev/hackathons)
- **File:** `hackathons_dataset.csv`
- **Size:** 10,179 rows, 11 columns
- **Columns:** `name`, `organization_name`, `location`, `themes`, `submission_start_date`, `submission_end_date`, `prize_currency`, `prize_amount`, `registrations`, `invite_only`, `url`

Note: this covers hackathons **listed on Devpost**, not every hackathon in the world.

## Questions

1. Which year was the peak for hackathons?
2. How have topics (themes) trended over time?
3. How has participation (registrations) changed?

## Tools

Python, pandas, NumPy, matplotlib, kagglehub, Jupyter Notebook

## Data Cleaning

| Issue | Action |
|---|---|
| Dates stored as text (`Oct 01, 2024`) | Converted to datetime; added `start_year` |
| 1 missing `name` | Filled from the URL ("She Innovates 2022") |
| 170 missing `location` | Filled with `"Unknown"` |
| 4,310 missing `themes` | Filled with `"Unknown"`; rows kept for peak and participation |
| ~5,085 missing `organization_name` | Left as is (not used in the analysis) |
| `themes` holds several values in one cell | Split into `themes_list`; exploded into a separate `themes_df` (one row per theme) |
| 9 negative `registrations` | Dropped 8 test entries; set 1 unclear row to NaN |
| 15 rows with 0 `registrations` | Dropped 4 junk/test rows and 2 cancelled/old listings; set the remaining 9 to NaN (not recorded) |
| 1 row with end date before start date | End date set to NaT; row kept |
| Extra spaces in text columns | Stripped |
| Mixed currencies in `prize_currency` | Not cleaned, since prizes are not part of the questions. Compare within `$` only if prizes are analyzed later |

Final cleaned dataset: **10,165 rows**.

## Key Findings

- **Peak year:** 2024, with 1,327 hackathons listed. Growth was steady from 2014 onward, with only a flat period between 2021 (1,198) and 2022 (1,185).
- **Theme data limitation:** themes are mostly missing before 2021 (95-100% missing through 2017, 41% missing in 2020, 0% from 2022). Topic trends are only reliable for 2022-2024 (2021 with a caveat).
- **Topic trend (2022-2024):** Machine Learning/AI grew fastest (146 to 396 tags), while hackathons overall grew about 12%. Beginner Friendly is the largest theme. Social Good, Education and Open Ended are flat or slightly down.


Theme counts are tags, not hackathons. A hackathon with 3 themes is counted once in each.

## How to Run

```bash
pip install kagglehub pandas numpy matplotlib
```

Open the notebook and run all cells from the top (`Kernel -> Restart & Run All`). The notebook downloads the dataset with `kagglehub`, so no manual download is needed.

## Project Structure

```
.
├── README.md
├── dA_HACKATHON.ipynb
└── hackathons_clean.csv      # cleaned data (optional export)
```

## Limitations

- Devpost listings only, not all hackathons worldwide.
- Registrations are sign-ups, not unique people.
- Prize amounts are in mixed currencies and were not converted.
- Missing themes before 2021 make early topic trends unreliable.
