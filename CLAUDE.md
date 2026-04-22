# CLAUDE.md

This file documents the codebase for AI assistants working in this repository.

## Project Overview

**Name:** training-room-app ("Trainingsraum")  
**Description:** A web application for a training room. Currently an early-stage skeleton with the core server and frontend stubs in place.  
**Status:** Active development — most features are not yet implemented.

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Runtime | Node.js |
| Backend framework | Express.js 4.18.2 |
| Database | SQLite3 5.1.6 (declared, not yet integrated) |
| Middleware | CORS 2.8.5, body-parser 1.20.2 |
| Configuration | dotenv 16.0.0 (declared, not yet used) |
| Frontend | HTML5, plain CSS, vanilla JavaScript |

## Directory Structure

```
Room/
├── server.js        # Express server — serves public/ on port 3000
├── app.js           # Client-side JS entry point (stub)
├── index.html       # Root HTML page
├── styles.css       # Global stylesheet (dark theme)
├── package.json     # Project metadata and dependencies
└── README.md        # Empty — not yet written
```

> **Note:** The server references a `public/` directory (`express.static('public')`) that does not yet exist. Static assets (HTML, CSS, JS) for the frontend should be placed there.

## Development Commands

```bash
# Install dependencies
npm install

# Start the development server
npm start
# → Server runs on http://localhost:3000
```

No other scripts are configured. There is no test runner, linter, or build step at this time.

## Key Files

### `server.js`
The Express application entry point. Serves static files from the `public/` directory and listens on port 3000. Currently minimal — no routes, no middleware, no database connection.

```js
const express = require('express');
const app = express();
app.use(express.static('public'));
app.listen(3000, () => console.log('Running on 3000'));
```

### `app.js`
Intended as the client-side JavaScript entry point. Currently only contains a console log stub. Should be placed inside `public/` or linked from `index.html` once the static directory is set up.

### `index.html`
Minimal HTML document displaying the "Trainingsraum" heading. Needs to be moved into `public/` to be served by the Express static middleware.

### `styles.css`
Single-rule dark theme: `background:#111; color:#fff; font-family:sans-serif`. Needs to be moved into `public/` alongside `index.html`.

## Dependencies

| Package | Purpose |
|---------|---------|
| `express` | HTTP server and routing |
| `cors` | Enable Cross-Origin requests (not yet wired up) |
| `body-parser` | Parse JSON/form request bodies (not yet wired up) |
| `sqlite3` | Local relational database (not yet integrated) |
| `dotenv` | Load `.env` config into `process.env` (not yet used) |

## Code Conventions

- **Modules:** CommonJS (`require` / `module.exports`) for server-side code.
- **Style:** Compact, minimal formatting (no spaces around `=` in current server.js). New code should follow standard JS style with spaces around operators and after keywords.
- **Naming:** camelCase for variables and functions; lowercase for filenames.
- **CSS:** Single dark theme palette (`#111` background, `#fff` text). Extend with CSS custom properties (`--var`) rather than repeating raw values.
- **No linter or formatter is configured.** Consider adding ESLint + Prettier before the codebase grows.

## Known Gaps and TODOs

- `public/` directory does not exist — the server cannot serve files until it is created and populated.
- `sqlite3`, `cors`, `body-parser`, and `dotenv` are installed but not used anywhere.
- No `.gitignore` — `node_modules/` and any future `.env` files should be ignored.
- No test framework or test files exist.
- No environment variable configuration (`.env.example` should be added when `dotenv` is wired up).
- `README.md` is empty.

## AI Assistant Guidelines

- **Before adding routes or middleware**, wire up the existing declared dependencies (`cors`, `body-parser`, `dotenv`) in `server.js` rather than adding new packages.
- **Database work:** Initialize SQLite3 with a schema file (e.g., `db/schema.sql`) and a setup script before writing queries.
- **Frontend assets** belong in `public/` — move or create `index.html`, `styles.css`, and `app.js` there so Express can serve them.
- **Do not add a build tool** (Webpack, Vite, etc.) unless the user explicitly requests one; the project is intentionally simple.
- **Tests:** If adding tests, use Jest (common in the Node.js ecosystem) and add a `"test": "jest"` script to `package.json`.
- **Environment variables:** Never hardcode secrets. Use `.env` (gitignored) and document keys in `.env.example`.
- **Port:** The server runs on port 3000. If making it configurable, use `process.env.PORT || 3000`.
