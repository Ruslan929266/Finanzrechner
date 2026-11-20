# Finanzrechner

A simple bookkeeping calculator for the browser: record business transactions, and the journal, general ledger, balance sheet and income statement are created automatically. The chart of accounts is based on the Swiss SME chart of accounts (KMU-Kontenrahmen). Everything lives in a single HTML file, with no build step and no server.

## Getting started

1. Open `Finanzrechner.html` in your browser (a double-click is enough).
2. Go to **Geschäftsfälle** and click "Beispiel laden" (load example), or enter your first bookings yourself.
3. Open **Bilanz und Erfolgsrechnung** to see the result.

Your data stays in the browser (`localStorage`). It never leaves your device unless you export it. The interface is in German.

## Features

### Booking
- **Record a transaction:** description, debit account (Soll), credit account (Haben), amount, month and day (the year comes from the selected period).
- **Journal:** all bookings with date, debit, credit and amount. Bookings can be **edited** and **deleted**.
- **Opening balances:** book them against account `9100 Eröffnungsbilanz` (assets on the debit side, liabilities and equity on the credit side), or enter them directly in the account management.

### Reports
- **Balance sheet in account form** as of the end of the selected period: current assets, fixed assets, short-term and long-term liabilities, and equity (including the cumulative profit or loss). The app tells you whether the balance sheet balances.
- **Income statement** (single-step) for the selected period only, split into operating and non-operating ("neutral") areas. Accounts whose number starts with `7` or `8` count as non-operating.
- **General ledger:** every account as a T-account with debit and credit, counter account and balance (`SBi` for balance sheet accounts, `ER` for income statement accounts).

### Time
- Years can be added, and months are chosen with chips (or "Ganzes Jahr", the whole year).
- Every month has **30 days** and a year has **360 days**, so a year ends on 30 December.

### Terms and maturities
- **Adjustable limits:** "Fremdkapital ist langfristig ab (Monate)" (liabilities are long-term from) and "Aktivum ist Anlagevermögen ab (Monate)" (an asset counts as fixed from), both 12 months by default.
- **Term from – to** (in months from the start of the first year) is available for accounts of type *Anlagevermögen (mit Laufzeit)* and *Langfristiges Fremdkapital (mit Laufzeit)*.
- The remaining term changes with the selected period. A loan with less than 12 months left moves to short-term liabilities automatically, and a fixed asset with too short a remaining term moves to current assets.

### Account management
- **Add** and **delete** your own accounts. An account used in bookings can only be deleted once those bookings are deleted.
- Types: current assets, fixed assets (with term), short-term liabilities, long-term liabilities (with term), equity, revenue, expense.
- Company name for the titles of the balance sheet and income statement.

### Presets
A preset contains accounts, terms and settings, and optionally the bookings as well.
- Save to the list and/or as a `.json` file.
- Load from the list, from a file or from a whole folder.
- Delete from the list (with confirmation).

### Export
Menu item **Export**: choose the period (from/to) and the format.

| Format | Content |
| --- | --- |
| Excel (`.xlsx`) | four sheets: journal, trial balance, income statement, balance sheet |
| CSV (`.csv`) | the same four parts one below the other, separator `;` |
| JSON (`.json`) | the same sheets as a data structure |

Journal and trial balance cover the selected period. The balance sheet shows the position at the end of the period.

### Colour themes
- Appearance: automatic (system), light or dark.
- Set your own colours for light and dark, save them as a theme, apply or delete them.
- Share as a `.json` file (download, file and folder import) or as a text code.
- Three themes are included: Standard, Ozean, Bordeaux.

## Default chart of accounts (KMU-Kontenrahmen)

The app starts with the following accounts, a compact selection from the Swiss SME chart of accounts. Account names stay in German, as is usual in Swiss bookkeeping. You can add or delete accounts at any time. "Term" is the default term in months for accounts with a term.

### 1 – Assets (Aktiven)

| No. | Account | English | Type | Term |
| --- | --- | --- | --- | --- |
| 1000 | Kasse | Cash | Current assets | – |
| 1020 | Bank | Bank | Current assets | – |
| 1060 | Wertschriften | Securities | Asset with term | 6 |
| 1100 | Forderungen aus L+L | Trade receivables | Current assets | – |
| 1170 | Vorsteuer | Input VAT | Current assets | – |
| 1200 | Handelswaren | Merchandise inventory | Current assets | – |
| 1300 | Aktive Rechnungsabgrenzung | Prepaid expenses and accrued income | Current assets | – |
| 1440 | Darlehensforderungen | Loan receivables | Asset with term | 36 |
| 1500 | Maschinen und Apparate | Machinery and equipment | Asset with term | 60 |
| 1510 | Mobiliar und Einrichtungen | Furniture and fixtures | Asset with term | 96 |
| 1520 | Büromaschinen und IT | Office machines and IT | Asset with term | 36 |
| 1530 | Fahrzeuge | Vehicles | Asset with term | 60 |
| 1600 | Immobilien | Real estate | Asset with term | 240 |

### 2 – Liabilities and equity (Passiven)

| No. | Account | English | Type | Term |
| --- | --- | --- | --- | --- |
| 2000 | Verbindlichkeiten aus L+L | Trade payables | Short-term liabilities | – |
| 2100 | Bankverbindlichkeiten | Bank liabilities | Liability with term | 6 |
| 2200 | Geschuldete MWST | VAT payable | Short-term liabilities | – |
| 2300 | Passive Rechnungsabgrenzung | Accrued expenses and deferred income | Short-term liabilities | – |
| 2400 | Darlehensschulden | Loans payable | Liability with term | 36 |
| 2420 | Hypothek | Mortgage | Liability with term | 240 |
| 2800 | Eigenkapital | Equity | Equity | – |

### 3 – Revenue (Ertrag)

| No. | Account | English | Area |
| --- | --- | --- | --- |
| 3200 | Handelserlöse | Merchandise revenue | Operating |
| 3400 | Dienstleistungserlöse | Service revenue | Operating |
| 3600 | Übrige Erlöse | Other revenue | Operating |
| 6950 | Finanzertrag | Financial income | Operating |
| 8100 | Betriebsfremder Ertrag | Non-operating income | Non-operating |

### 4–6, 8 – Expenses (Aufwand)

| No. | Account | English | Area |
| --- | --- | --- | --- |
| 4200 | Warenaufwand | Cost of goods | Operating |
| 5000 | Lohnaufwand | Wages and salaries | Operating |
| 5700 | Sozialversicherungsaufwand | Social security expense | Operating |
| 6000 | Raumaufwand | Premises expense (rent) | Operating |
| 6100 | Unterhalt und Reparaturen | Maintenance and repairs | Operating |
| 6200 | Fahrzeugaufwand | Vehicle expense | Operating |
| 6300 | Versicherungen | Insurance | Operating |
| 6400 | Energie und Entsorgung | Energy and disposal | Operating |
| 6500 | Verwaltungsaufwand | Administration expense | Operating |
| 6600 | Werbeaufwand | Advertising expense | Operating |
| 6800 | Abschreibungen | Depreciation | Operating |
| 6900 | Finanzaufwand | Financial expense | Operating |
| 8000 | Betriebsfremder Aufwand | Non-operating expense | Non-operating |

### Special account

| No. | Account | Purpose |
| --- | --- | --- |
| 9100 | Eröffnungsbilanz | Counter account for opening balances (not shown in the reports) |

## Notes

- The Excel export loads the library [SheetJS](https://sheetjs.com) from `cdnjs.cloudflare.com` and therefore needs an internet connection. CSV and JSON also work offline.
- Data is stored under these `localStorage` keys: `fr1` (bookings, accounts, settings), `finanz_presets` (presets) and `finanzrechner_themes` (colour themes). Clearing the browser storage deletes them, so save important states as a preset with bookings or as an export.
- There is no built-in PDF export.

## License

MIT, see [LICENSE](LICENSE).
