# Nepal Hydropower Data Analysis

Data cleaning, transformation, exploratory data analysis (EDA) and visualization of Nepal's hydropower licence
register (572 records, 14 columns), built with Python, Pandas, Matplotlib, Seaborn.

## Project structure


nepal-hydropower-analysis/
├── notebooks/
│   └── Nepal_Hydropower_Data_Analysis.ipynb   # full analysis, documented step by step
├── data/
│   ├── hydropower.csv                         # raw data (add this file yourself)
│   ├── nepal_hydropower_cleaned.csv           # output: cleaned dataset
│   └── nepal_hydropower_model_ready.csv       # output: encoded + scaled dataset
├── figures/                                   # output: every chart, saved as PNG
├── requirements.txt
└── README.md


## Setup


git clone https://github.com/<Basanta-sapkota09>/nepal-hydropower-analysis.git
cd nepal-hydropower-analysis

python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# put hydropower.csv in the data/ folder, then:
jupyter notebook notebooks/Nepal_Hydropower_Data_Analysis.ipynb
```

Choose **Kernel > Restart & Run All**. The notebook also runs in Google Colab: upload `hydropower.csv`
and run all cells.

## Dataset

| Column | Description |
|---|---|
| Project, River, Promoter | Project name, river and developer |
| Province, District, Municipality, Address | Location in administrative terms |
| Capacity (MW) | Installed or proposed capacity |
| Lic No, Isuue Date, Validity | Licence number, issue date, validity (Bikram Sambat calendar) |
| Longitude, Latitude | Project coordinates |
| License Type | Survey, Generation or Operation |

## What the notebook does

1. **Exploration:** structure, data types, summary statistics, quality checks.
2. **Cleaning and transformation:**
   * placeholder values (`0`, `1_gtd`, `0/1/0`) converted to missing and labelled `Unknown`,
   * Bikram Sambat dates parsed into year and licence term,
   * outliers flagged with the IQR rule, kept, and capacity log-transformed,
   * new features: capacity category, province name, NEA promoter flag, storage-project flag, licence term,
   * one-hot and ordinal encoding, standard scaling.
3. **EDA:** distributions, capacity by licence type, province and river, geography, licences over time,
   pair plot, Pearson and Spearman correlations.
4. **Feature selection:** mutual information and random-forest importance, with leakage excluded.
5. **Insights and recommendations.**

## Key findings

* Capacity is heavily skewed: median 9.2 MW versus mean 41.9 MW, maximum 1,902 MW.
* 55% of records are small projects (10 MW or less); 74 records (12.9%) are statistical outliers.
* 54% of records hold Survey licences, so most of the pipeline is still at an early stage.
* Provinces 4, 3 and 1 account for 86% of records.
* The data has hidden quality problems: 60 placeholder licence numbers, BS-calendar dates, and 40 unusable validity values.

## Publishing to GitHub


git init
git add .
git commit -m "Add Nepal hydropower data analysis"
git branch -M main
git remote add origin https://github.com/<Basanta-sapkota09>/nepal-hydropower-analysis.git
git push -u origin main
```

Create the empty repository on github.com first. Commit the notebook **after running it**, so the saved plots
render on GitHub, and include the generated cleaned CSV files.
