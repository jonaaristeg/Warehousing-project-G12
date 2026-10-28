# Warehousing project (WH-FINAL), group 12

Management report on storage, layout and order picking at the S. P. Richards DC.

## Setup
Python 3.10 to 3.13 (not 3.14 or newer: matplotlib 3.10.7 has no prebuilt package there) and TeX Live with IEEEtran (`texlive-publishers`, `texlive-bibtex-extra`; included in Overleaf).

    python3 -m venv .venv   # Windows: py -3.12 -m venv .venv
    ./.venv/bin/python -m pip install -r requirements-notebook.txt
    ./.venv/bin/python -m ipykernel install --sys-prefix --name warehouse-project

Windows: use `python` and `.\.venv\Scripts\python.exe`.

## Generate the evidence
One command, from the project root (`run.sh` / `run.cmd` do the same):

    ./.venv/bin/python -m nbconvert --config notebook_config.py

It executes `analysis.ipynb` from start to finish. The code reads the original files in `data/raw/`, downloads missing ones from the approved course source and checks their SHA-256 hashes (`data/sources.json`, needs internet on the first run), and saves every table (`.csv`, report tables also `.tex`) and figure (`.png`, `.pdf`) in `artifacts/`. Scenarios S0 to S7 are generated in the notebook from three on/off decisions; their definitions, settings, feasibility and results are saved in `artifacts/as5_scenario_*.csv` and `as5_table_summary.csv`. The only random step uses fixed seeds 0 to 4. The run takes several minutes (large sales file). Raw data is not committed.

## Compile the report
The finished tables and figures are already in `artifacts/`.

    cd report
    latexmk -pdf main.tex

(or pdflatex, bibtex, pdflatex, pdflatex). The result is `report/main.pdf` (limit: 12 pages).
