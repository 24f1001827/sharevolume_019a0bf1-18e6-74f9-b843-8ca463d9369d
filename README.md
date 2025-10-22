# Aflac Shares Outstanding Web App

This small web application fetches and displays the maximum and minimum shares outstanding numbers for a given company's common stock as reported in SEC filings. It uses live data from the SEC's public XBRL API.

---

## Summary

The app initially loads data for Aflac, Inc. (CIK 0000004977) and displays its entity name alongside the maximum and minimum shares outstanding for fiscal years after 2020. Users can dynamically query other companies' data by specifying a 10-digit CIK in the URL query string, for example: `index.html?CIK=0001018724`.


## Setup

No build or server setup is required. Simply open the `index.html` file in a modern web browser. The app uses native `fetch` to retrieve data from the SEC public API.


## Usage

- Open `index.html` normally to view Aflac's latest shares outstanding data.
- To view data for another company, append `?CIK=XXXXXXXXXX` to the URL, where `XXXXXXXXXX` is a 10-digit SEC CIK number (e.g., `?CIK=0001018724`). The page will fetch and display that company's data dynamically without reloading.


## Code Explanation

### Files

- `index.html`: The main web page that displays the shares outstanding data. It includes:
  - A `<title>` and `<h1>` incorporating the entity name.
  - Marked elements with IDs:
    - `share-entity-name` — displays the company/entity name.
    - `share-max-value`, `share-max-fy` — display the max shares value and fiscal year.
    - `share-min-value`, `share-min-fy` — display the min shares value and fiscal year.
  - JavaScript that:
    - Parses the CIK from the URL if present.
    - Fetches data from SEC API with a descriptive `User-Agent` header.
    - Filters and processes JSON data to find max/min shares outstanding values for FY after 2020.
    - Dynamically updates all relevant DOM elements and page title.

- `data.json`: A static snapshot example of Aflac's data used for reference.

- `uid.txt`: Some attached identifier file as provided.


### Data Fetch & Processing

- Fetches from:
  `https://data.sec.gov/api/xbrl/companyconcept/CIKXXXXXXXXXX/dei/EntityCommonStockSharesOutstanding.json`
- Filters for fiscal years (`fy`) > "2020" and ensures shares are numeric.
- Finds entries with the maximum and minimum number of shares outstanding.


### Rendering

- The UI updates the textContent of the designated IDs to current data.
- The page title reflects the current entity name.


## Notes

- The User-Agent header follows SEC guidance for API access.
- The app features basic styling for clarity and visual appeal.
- Error handling fallbacks default to Aflac data if fetching for alternate CIK fails.

---

This app is a simple demonstration of live financial data visualization from the SEC's EDGAR system.