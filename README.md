# Energy Community Maturity Check

Self-assessment tool of the **ECHO Community Benchmarking and Learning Toolkit** (deliverable D3.2, Horizon Europe grant agreement No 101185725). An energy community answers 20 questions in five areas and gets:

- a maturity score (1–5) for each area and overall,
- its stage (emerging, early-stage or mature),
- a comparison with the average of the ECHO pilot communities,
- suggested next steps, with links to learning material.

> **Status: prototype.** The questions are a starting draft and the benchmark values are illustrative, not real pilot results.

## How it works

The tool is a single web page (`index.html`) that reads all its content from CSV files in the `data` folder. There is no server, no database and no login. All calculations run in the visitor's browser, and **no answers are sent anywhere**. The page only remembers the answers in the visitor's own browser, so they can continue later on the same device.

```
index.html            the page (no need to edit)
data/ui.csv           interface text, one column per language
data/dimensions.csv   the five areas, their short names and weights
data/questions.csv    the questions and the description of each of the five levels
data/stages.csv       the maturity stages and the score at which each starts
data/benchmarks.csv   average score per stage and area (from the pilots, Task 3.3)
data/advice.csv       next-step advice per area and score band, with a learning link
data/example.csv      answers of the fictional example community
```

## Editing the content (no programming)

1. Open the CSV file in Excel or LibreOffice.
2. Change the text or numbers. **Do not rename the column headers or the ids** (G1, GOV, early, and so on).
3. Save as **CSV UTF-8**. Semicolon-separated files and decimal commas (2,25) from a Greek Excel also work.
4. Upload the file to GitHub (see below) to replace the old one. The site updates within a minute or two.

Common changes:

- **Add or remove a question:** add or delete a row in `questions.csv`. The `dimension` column says which area it belongs to; `weight` is normally 1.
- **Change the stage thresholds:** edit `min_score` in `stages.csv`.
- **Put in real benchmarks:** replace the values in `benchmarks.csv` with the averages of the pilot communities at each stage, set `n` to the number of communities, and change `source` from `illustrative` to, for example, `ECHO pilots 2027`.
- **Add a learning link:** paste the address of the training module or document in `link_url` in `advice.csv`.
- **Add a language (e.g. Turkish):** add a `tr` column to `ui.csv` and `_tr` columns next to the `_en` ones in the other files (`question_tr`, `level1_tr` … `level5_tr`, `name_tr`, `short_tr`, `description_tr`, `advice_tr`, `link_label_tr`). The language button appears automatically. Missing translations fall back to English.

## Scoring rules

- Each answer is a level from 1 to 5. "Don't know / not applicable" is left out of the calculation.
- Area score = weighted average of the answered questions in that area.
- Overall score = weighted average of the area scores (weights in `dimensions.csv`).
- Stage = the highest stage whose `min_score` is at or below the overall score.
- Advice = for each area, the first row in `advice.csv` whose `max_score` is at or above the area score. Areas are listed weakest first.

## Publishing on GitHub Pages (free)

1. Create a GitHub account (or an organisation, for example `echo-energy-communities`) at <https://github.com>.
2. Click **New repository**, name it `maturity-check`, set it to **Public** and create it.
3. Click **Add file → Upload files**, drag in `index.html`, `README.md`, `LICENSE` and the `data` folder, then click **Commit changes**.
4. Go to **Settings → Pages**. Under *Build and deployment*, choose **Deploy from a branch**, branch **main**, folder **/ (root)**, and save.
5. After a minute the tool is online at `https://<account>.github.io/maturity-check/`.

To test on your own computer instead, open a terminal in this folder, run `python -m http.server`, and open <http://localhost:8000>. Opening `index.html` by double-clicking does not work, because the browser blocks it from reading the CSV files.

## Archiving on Zenodo (DOI for each release)

As set out in the ECHO Data Management Plan:

1. Log in to <https://zenodo.org> with your GitHub account.
2. In Zenodo, open **Account → GitHub** and switch on the `maturity-check` repository.
3. In GitHub, create a **Release** (for example `v0.1.0-alpha`). Zenodo archives it automatically and gives it a DOI.
4. Ask IDI to add the record to the ECHO community: <https://zenodo.org/communities/echoenergycom>.

## Before the public release

- [ ] Replace the sample questions with the indicator set agreed with NOVA and QUE (Task 3.3) and map them to the Energy Communities Repository indicators.
- [ ] Replace the illustrative benchmarks with real, anonymised pilot averages.
- [ ] Add the learning links (ECHO training platform, case studies, D5.2, D3.3).
- [ ] Add Turkish and Portuguese, and have the Greek text proofread.
- [ ] Add the EU emblem next to the funding statement.
- [ ] Decide whether to host the fonts on the site itself instead of loading them from Google Fonts, to avoid sending visitors' IP addresses to Google.
- [ ] Confirm the copyright holder in `LICENSE` with the consortium.
- [ ] Run an accessibility check (keyboard use, screen reader, contrast).

## Licence

Code: MIT (see `LICENSE`). Content and data in `data/`: CC BY 4.0. In line with the licence policy of the ECHO Data Management Plan.

Funded by the European Union under grant agreement No 101185725 (ECHO). Views and opinions expressed are however those of the author(s) only and do not necessarily reflect those of the European Union or the European Research Executive Agency (REA). Neither the European Union nor the granting authority can be held responsible for them.
