# Quicklite viewer
A tiny & fast SQLite desktop viewer

This is a **single‑file**, **read‑only bydefault** SQLite viewer built with Python and Tkinter.

It deliberately avoids bloat: you drop in a `.db` / `.sqlite` file, and you’re browsing tables, writing queries with lightweight assistance, and exporting results.

The goal is to **feel as light as a terminal, but with just enough UI to make day‑to‑day inspection faster and less error‑prone.**

---

## Highlights

- **Small & lightweight**
  - Single Python script, standard‑library only (plus `tkinter` and `sqlite3`).
  - Starts in a fraction of a second on modest hardware.
  - No installers, no services, no telemetry.

- **Fast table browsing**
  - Paging with adjustable page size (`100 / 200 / 500 / 1000` rows).
  - Clickable column headers for sorting (ASC/DESC) without rewriting your query.

- **Safe by default**
  - **Read‑only mode is the default.**
  - In read‑only mode, the query runner only accepts `SELECT` and `PRAGMA` statements.

- **Helpful, but not heavy, query tools**
  - Lightweight **syntax highlighting** for common SQL keywords (`SELECT`, `FROM`, `WHERE`, `LIKE`, etc.)
  - **Contextual suggestions** on `Ctrl+Space`:
    - Suggest table names after `FROM`, `JOIN`, `UPDATE`, `INTO`.
    - Suggest column names based on the currently selected table.
    - Suggestions are schema‑aware but deliberately simple. This is not a full SQL IDE.

- **Data inspection quality‑of‑life**
  - Right‑click on a column header to **hide/show columns** without touching the query.
  - **Clickable URLs**: cells that look like `http://...` or `https://...` open in your default browser.
  - Export **current result grid** (what you see) to:
    - CSV (with header row)
    - TXT (tab‑separated)

---

## Why this exists

There are many SQLite viewers already, but I didn't need a bloated full-IDE nor a barebone browser, so this small tool occupies the middle ground:

- It **does not** try to be an IDE.
- It **does** try to remove the most tedious parts of “just looking at a database”:
  - remembering exact table/column names,
  - copy‑pasting ad‑hoc query results,
  - scrolling through irrelevant columns,
  - accidentally mutating data you only meant to inspect.

If you already live in a terminal or heavy SQL client all day, this is meant to be the small, fast thing you open for “let me quickly check that table”.

---

### Query editor

The parser is deliberately modest: it doesn’t try to understand complex joins, aliases, or nested queries. That keeps the implementation small and robust while still giving a real speed boost for everyday queries.

### Result grid

The grid is tuned for inspection, not editing:

- **Column hiding/showing:**
  - Right‑click on any header to hide it.
  - Use the same menu to bring hidden columns back.
  - Hidden state is per‑result; queries that change the schema reset visibility.
- **URL detection:**
  - Any cell starting with `http://` or `https://` is treated as a link.
  - Hovering shows a hand cursor; clicking opens the URL in your browser.
- **Export:**
  - The **currently visible grid** (whatever query or table page you see) can be exported as:
    - CSV – standard comma‑separated with header row.
    - TXT – tab‑separated with header row.
  - Exports don’t try to be clever; “what you see is what you get”.

---

## Installation

Requirements:

- Python 3.10+ (earlier versions may work, but are not tested).
- `tkinter` available in your Python installation.
- No third‑party libraries required.

Clone or copy the script and run:

```bash
python sqlite_viewer.py
