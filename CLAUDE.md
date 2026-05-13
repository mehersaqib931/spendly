# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Spendly** — a Flask/SQLite expense-tracking web app. This is a student coding project scaffold; `database/db.py` and `static/js/main.js` are stubs meant to be filled in as exercises.

## Commands

```bash
# Create and activate virtual environment (first time)
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # macOS/Linux

# Install dependencies
pip install -r requirements.txt

# Run the dev server (once app.py exists)
flask run
# or
python app.py

# Run all tests
pytest

# Run a single test file
pytest tests/test_auth.py

# Run a single test by name
pytest -k "test_login"
```

## Architecture

### Stack
- **Backend**: Flask 3.1.3, Python, SQLite (via stdlib `sqlite3`)
- **Templates**: Jinja2 (extends `templates/base.html`)
- **Frontend**: Vanilla JS (`static/js/main.js`), plain CSS (`static/css/style.css`)
- **Testing**: pytest + pytest-flask

### Key conventions
- `database/db.py` must expose three functions: `get_db()`, `init_db()`, `seed_db()`. `get_db()` should enable `row_factory` (so rows behave like dicts) and `PRAGMA foreign_keys = ON`.
- The SQLite database file is `expense_tracker.db` at the project root (gitignored).
- All routes live in `app.py` (not yet created); URL endpoints are referenced in templates via `url_for('landing')`, `url_for('login')`, `url_for('register')`.
- Currency is Indian Rupee (₹) throughout.
- Templates use a shared `base.html` that injects the navbar, footer, Google Fonts (DM Serif Display + DM Sans), and the global CSS/JS files.

### Template structure
`base.html` provides `{% block title %}`, `{% block head %}`, `{% block content %}`, and `{% block scripts %}` extension points. All pages extend it.
