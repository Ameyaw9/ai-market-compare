# AI Market Compare

A small Flask app that compares two AI companies by market capitalisation. Pick any two companies and it shows a size comparison drawn to scale, a stats table, a short plain-English analysis, a brief description of each company (from Wikipedia), and a link to compare them on Google.

> **Data note:** all figures come from the data sheet in `data/companies.csv`, which is a snapshot **as at 1 October 2026** (source: companiesmarketcap.com, "Largest AI companies by market capitalization"). Market caps and prices are not live and will not update on their own.

## Requirements

- Python 3.9 or newer
- An internet connection (only needed for the Wikipedia descriptions; the rest works offline)

## Run it locally

1. **Open a terminal in the project folder** (the one containing `app.py`).

2. **Create a virtual environment**

   macOS / Linux:
   ```bash
   python3 -m venv .venv
   ```
   Windows:
   ```bat
   python -m venv .venv
   ```

3. **Activate it**

   macOS / Linux:
   ```bash
   source .venv/bin/activate
   ```
   Windows (Command Prompt):
   ```bat
   .venv\Scripts\activate
   ```
   Windows (PowerShell):
   ```powershell
   .venv\Scripts\Activate.ps1
   ```

4. **Install the dependencies**
   ```bash
   pip install -r requirements.txt
   ```

5. **Start the app**
   ```bash
   flask --app app run --debug
   ```

6. **Open it in your browser** at http://127.0.0.1:5000

7. **Stop it** with `Ctrl + C` in the terminal. Run `deactivate` to leave the virtual environment.

## Using the app

- Choose a company in each dropdown and press **Compare**.
- The URL updates (for example `/?a=NVDA&b=AAPL`), so you can bookmark or share a comparison.
- JSON version: `http://127.0.0.1:5000/api/compare?a=NVDA&b=AAPL`

## Project structure

```
ai-market-compare/
├── app.py              # Flask routes, analysis logic, Wikipedia lookup
├── requirements.txt
├── data/
│   └── companies.csv   # market cap snapshot, 1 October 2026
├── templates/
│   └── index.html
└── static/
    └── style.css
```

## Updating the data

Export a fresh CSV from companiesmarketcap.com, keep the same columns (`Rank, Name, Symbol, marketcap, price (USD), country`), replace `data/companies.csv`, restart the app, and update the date in this README and in `templates/index.html`.

## Troubleshooting

- **`flask: command not found`**: the virtual environment isn't active. Repeat step 3.
- **`Address already in use`**: another app is using port 5000. Run `flask --app app run --debug --port 5001` and open http://127.0.0.1:5001.
- **"Couldn't load a summary right now"**: the Wikipedia lookup failed (no internet, or a timeout). The rest of the page still works, and the Google links are unaffected.
- **A description is about the wrong company**: the lookup is a simple name search. The page shows which Wikipedia article it used, so check that link.
- **`python` not found on Windows**: try `py` instead of `python`.
