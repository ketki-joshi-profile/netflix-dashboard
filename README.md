# Netflix Titles Dashboard

An interactive Tableau dashboard that explores how Netflix's catalogue of movies and TV shows has grown over time, and how it breaks down by type, genre, country and rating.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Project Scope & Tools](#3-project-scope--tools)
4. [Repository Structure](#4-repository-structure)
5. [Data Workflow](#5-data-workflow)
6. [Data Model & Schema](#6-data-model--schema)
7. [Dashboard Design & Metrics](#7-dashboard-design--metrics)
8. [Key Insights](#8-key-insights)
9. [Assumptions & Limitations](#9-assumptions--limitations)
10. [Future Enhancements](#10-future-enhancements)
11. [Deliverables](#11-deliverables)
12. [How to Open the Dashboard](#12-how-to-open-the-dashboard)
13. [Author](#13-author)

---

## 1. Project Overview

**Context:** Netflix's catalogue is large and changes constantly, and a plain title list makes it hard to see the overall shape of the library. This project is a visualisation portfolio piece, built to practise dashboard design in Tableau.

**Problem Statement:** How has the catalogue grown over time, and how is it split by type, genre, country and rating? Which titles fit a given profile?

**Approach:** I connected Tableau to the Netflix titles dataset and built twelve linked views on one dashboard. Quick filters on title, type and date added let the viewer drill into any slice of the catalogue.

**Outcome:** A single-page, interactive dashboard with a timeline of titles added, rankings for genre, country and rating, a movie-versus-TV split, and a title lookup panel.

---

## 2. Objectives

- **Primary Objective:** Build one dashboard that answers "what does the Netflix catalogue look like?" without the viewer needing to read the raw data.
- **Secondary Objective 1:** Show change over time, using titles added per year.
- **Secondary Objective 2:** Compare the catalogue by genre, country and rating.
- **Secondary Objective 3:** Let the viewer look up individual titles and see their details.

---

## 3. Project Scope & Tools

### Scope

| Dimension | Details |
|---|---|
| **In Scope** | The Netflix titles dataset (movies and TV shows): type, title, director, cast, country, date added, release year, rating, duration, genre, description |
| **Out of Scope** | Viewing data, subscriber numbers, and ratings or reviews from outside the dataset. Data cleaning and splitting of multi-value fields are not done in this workbook (see Limitations). |
| **Time Period** | Titles added to the catalogue: [add first and last date_added from your CSV]. Project completed November 2026. |
| **Granularity** | One row per title. Views aggregate by year of date added, genre, country, rating and type. |

### Tools & Technologies

| Category | Tool(s) Used |
|---|---|
| **Data Storage** | CSV file (`netflix_titles.csv`) |
| **Data Processing** | None outside Tableau. The workbook reads the CSV directly. |
| **Analysis** | Tableau aggregations and quick filters |
| **Visualization** | Tableau Desktop (workbook saved in version 18.1): area, bar, map, circle and text views |
| **Version Control** | Git / GitHub |
| **Documentation** | Markdown |
| **Other** | None |

---

## 4. Repository Structure

```
netflix-titles-dashboard/
│
├── data/
│   └── netflix_titles.csv          # Source data (add this file before opening the workbook)
│
├── dashboards/
│   └── Netflix_Dashboard.twb       # Tableau workbook containing the dashboard
│
├── visuals/
│   └── dashboard.png               # Screenshot of the full dashboard
│
└── README.md                       # You are here
```

The workbook has no calculated fields, so there is no queries or scripts folder. `reports/`, `notebooks/` and `docs/` were not needed and are not included.

---

## 5. Data Workflow

```
[netflix_titles.csv]
        ↓
[Tableau data connection: 12 columns, no calculations]
        ↓
[Twelve worksheets, each with one measure and one dimension]
        ↓
[One dashboard with shared quick filters]
```

**Source:** `netflix_titles.csv`, the Netflix titles dataset from Kaggle [confirm source and download date]. Contains [add row count] titles.

**Ingestion:** Tableau text-file connection to the CSV, header row on, UTF-8 encoding, comma separator.

**Cleaning:** None applied in the workbook. The source data is used as delivered.

**Transformation:** None. The workbook has no calculated fields. Year grouping on `date_added` uses Tableau's date aggregation.

**Analysis:** Count of distinct titles by year, genre, country, rating and type. Quick filters on title, type and date added.

**Output:** One interactive dashboard, 1800 × 1000 pixels, fixed layout.

---

## 6. Data Model & Schema

**Dataset / Table:** `netflix_titles.csv` (single table)

| Field Name | Data Type | Description | Example Value |
|---|---|---|---|
| `show_id` | integer | Unique identifier for each title | `[example ID]` |
| `type` | string | `Movie` or `TV Show` | `Movie` |
| `title` | string | Title of the movie or show | `[example title]` |
| `director` | string | Director name(s). Blank for some titles | `[example]` |
| `cast` | string | Comma-separated list of cast members. Blank for some titles | `[example]` |
| `country` | string | Country or countries of production. Can be a comma-separated list | `[example country]` |
| `date_added` | date | Date the title was added to Netflix | `[example date]` |
| `release_year` | integer | Year the title was originally released | `[example year]` |
| `rating` | string | Content rating, such as TV-MA or PG-13 | `[example rating]` |
| `duration` | string | Runtime for movies (minutes) or seasons for TV shows. Mixed units in one field | `[e.g. 90 min or 2 Seasons]` |
| `listed_in` | string | Genre labels. Can be a comma-separated list | `[example genres]` |
| `description` | string | Short plot summary | `[example summary]` |

**Row count:** [add from CSV]
**Date range:** [add min and max of date_added]
**Key join / relationship:** None. Single table. `show_id` is unique per title.

Fill in the example values from your own CSV before publishing. Use non-sensitive values only.

---

## 7. Dashboard Design & Metrics

### Dashboard Layout

The dashboard is a single fixed-size page of twelve views:

| View | Shows | Mark | Filter |
|---|---|---|---|
| Total Movies & TV | Titles added per year | Area chart | Year of date added |
| Top 10 Genre | Ten genres with the most titles | Bar chart | Genre |
| By country | Titles per country on a map | Filled map | Map coordinates |
| Distribution | Share of movies vs TV shows | Circle | None |
| Ratings | Titles per content rating | Bar chart | Title, type |
| Ratings_ | Rating breakdown, filtered by selection | Bar chart | Title, type |
| Release year | Titles by release year | Bar chart | Title, type |
| Duration | Runtime or seasons for the selected title | Text | Title, type |
| Genre | Genre labels for the selected title | Text | Title, type |
| Date added | Date added for the selected title | Text | Title, type |
| Description | Title, type and plot summary for the selected title | Text | Title, type |
| Title lookup | Quick filters for title and type | Filter controls | Title, type |

### Analytical Approach

This is a descriptive dashboard. It doesn't test a hypothesis or fit a model. Each view answers one question directly: the area chart shows change over time, the bar charts rank categories, the map shows geography, and the text views show details for a selected title. Quick filters apply across the dashboard, so the viewer can drill down without leaving the page.

### Key Metrics Defined

| Metric | Plain-Language Definition | Why It Matters |
|---|---|---|
| **Titles** | Count of distinct `show_id` values | The size of the catalogue |
| **Titles added per year** | Count of titles grouped by year of `date_added` | Shows when the catalogue grew and when it slowed |
| **Share by type** | Count of titles for each `type` value | Shows how much of the catalogue is films versus series |
| **Titles per genre** | Count of titles for each `listed_in` value | Shows which genres are most represented |
| **Titles per country** | Count of titles for each `country` value | Shows where content comes from |
| **Titles per rating** | Count of titles for each `rating` value | Shows the age-rating mix of the catalogue |

### Methods Used

- Count distinct aggregation on `show_id` across all views
- Date grouping on `date_added` by year
- Dimension filters on `listed_in` and map coordinates
- Quick filters on title, type and date added, shared across views
- Text views for the selected title's details

---

## 8. Key Insights

These insights need the data. The workbook contains the view definitions but no data rows, so each finding must be read from the dashboard once `netflix_titles.csv` is in `data/`. Replace each bracketed prompt with the finding.

**Insight 1: [Headline on how the catalogue grew over time].**
[Read from the area chart: the year with the most titles added, and whether growth was steady or came in bursts. One short paragraph on what that suggests.]

**Insight 2: [Headline on the type mix].**
[Read from the distribution view: the share of movies versus TV shows, and whether the balance has shifted over time.]

**Insight 3: [Headline on genre concentration].**
[Read from the top 10 genre view: which genres lead, and how much of the catalogue they account for. Note that titles with several genres are counted under each one.]

**Insight 4: [Headline on country and rating].**
[Read from the map and ratings views: the countries with the most titles, and the most common rating.]

---

## 9. Assumptions & Limitations

### Assumptions

- The CSV is a complete snapshot of the catalogue at the time it was downloaded.
- `date_added` is the date a title was added to Netflix, not its release date.
- Each `show_id` is one title.

### Limitations

- **Multi-value fields are not split.** `listed_in` (genre) and `country` contain comma-separated lists. The top 10 genre view and the map treat each combination as one category. For example, "Dramas, International Movies" is counted separately from "Dramas", so single-genre totals are understated.
- **The map may not geocode multi-country entries.** The map uses Tableau's generated coordinates on the raw country text, so a title with several countries may not place correctly.
- **Duration mixes units.** Movies are in minutes and TV shows in seasons, in one text field. The Duration view can't compare them directly.
- **Blank fields.** Some titles have no director, cast or country. These show as blanks rather than being excluded.
- **Date added is not a release date.** A title can be added years after it was released, so the "titles added per year" view shows catalogue growth, not production volume.
- **No cleaning step is documented in the workbook.** Any cleaning has to happen before the CSV is loaded.

---

## 10. Future Enhancements

- Split `listed_in` and `country` into one row per value in a data preparation step, then rebuild the genre and map views on the split data. This fixes the multi-value limitation.
- Add a separate duration view for movies and TV shows, so each unit is compared on its own.
- Replace the generated map coordinates with a country-level join, so multi-country titles are handled explicitly.
- Add a one-line takeaway under each view, so the dashboard reads as a story on its own.
- Rename the worksheets for clarity and remove the duplicate `Ratings_` sheet.
- Publish the dashboard to Tableau Public and link it here.

---

## 11. Deliverables

| Deliverable | Description | Location |
|---|---|---|
| Dashboard workbook | Tableau workbook with twelve views and quick filters | `dashboards/Netflix_Dashboard.twb` |
| Source data | Netflix titles CSV used by the workbook | `data/netflix_titles.csv` (add) |
| Dashboard screenshot | Full-page image of the dashboard for this README | `visuals/dashboard.png` (add) |
| Published dashboard | Public link to the interactive version | [add Tableau Public link] |

---

## 12. How to Open the Dashboard

1. Download the repository and place `netflix_titles.csv` in `data/`.
2. Open `dashboards/Netflix_Dashboard.twb` in Tableau Desktop.
3. If Tableau reports a missing data source, go to **Data > Replace Data Source** and choose `data/netflix_titles.csv`.

The workbook was saved with a local file path, so step 3 is needed on any other computer.

---

## 13. Author

**Ketki Joshi**
Data Analytics and Operations professional. MSc Business Analytics, Queen's University Belfast (2024).

🔗 LinkedIn: https://www.linkedin.com/in/ketki-joshi-31051999kpj/
📧 ketkipjoshi31@gmail.com

Last updated: November 2026
