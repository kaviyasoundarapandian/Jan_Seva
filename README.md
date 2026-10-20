# Jan Seva

A mobile-first, installable web app (PWA) that puts everyday citizen services in one place: emergency help, problem reporting, government schemes and documents, health and care, transport, learning, and a friendly support chat called Nanba. It is built for ease of use, with large buttons, many Indian languages, read-aloud and voice input.

> Jan Seva is not a government app. It links to official portals and does not replace them.

## Features

- **Emergency:** SOS screen and one-tap calls to 112, 100, 101, 108, 1091, 1098, 14416 and others
- **Report a problem:** save a report with category, description, photo and location; track it in My Reports
- **Category pages:** disaster, necessities, transport and routes, health, government schemes, old age, news, pay and bills, savings, loans, government exams and jobs, documents and ID, legal help, blood donation, agriculture, tourism, post and courier, form filling, accessibility and more
- **My care:** diet plan, sleep, notes, water, steps and reminders
- **Nanba:** offline friendly chat with a crisis response (Tele-MANAS 14416 / 112); optional connection to your own AI service
- **Panchangam and calendar**
- **Languages:** English, Hindi and many Indian languages (translation through Google Translate when online)
- **Accessibility:** read-aloud, voice input, light and dark mode
- **Security:** optional PIN, password and 2-step verification (TOTP)
- **Offline-first:** your data stays on your phone (browser `localStorage`)

## Tech stack

Plain HTML, CSS and vanilla JavaScript in a single `index.html`. No build step, no framework, no server, no database.

## Quick start

Requirements: any modern browser. For local testing, Python 3 or Node.js (any static file server will do).

```bash
git clone https://github.com/<your-username>/jan-seva.git
cd jan-seva

# Option A: Python
python3 -m http.server 8080

# Option B: Node.js
npx serve .
```

Open http://localhost:8080 in Chrome (use device mode in DevTools for a phone view).

The app registers a service worker, which only works on `http://localhost` or HTTPS. Opening `index.html` directly from disk (`file://`) works, but without install/offline support.

### Required files next to `index.html`

| File | Purpose |
|------|---------|
| `manifest.webmanifest` | PWA name, icons, theme colour |
| `sw.js` | service worker for offline support |

Both are referenced by `index.html`. Make sure they are in the repository root.

## Environment variables and configuration

Jan Seva runs entirely in the browser, so there are **no environment variables and no secrets** to set.

| Setting | Where | Required | Description |
|---------|-------|----------|-------------|
| Nanba AI endpoint | In the app: Nanba, then "Connect a real AI (optional)" | No | An `https://` URL of your own server. The app sends `{system, messages}` by POST and expects `{"reply": "..."}`. Stored as `ns_nb_api` in localStorage |
| Language | In the app header | No | Stored as `ns_lang` / `ns_ul` |

**Never put API keys in the front-end code.** If you use an AI service, keep keys on your own server and expose only the endpoint above.

If you run your own AI service, keep its key on your server (for example as an environment variable such as `AI_API_KEY`) and expose only the `https://` endpoint above to the app.

## Sample data and tests

- `sample-data/` has demo profile, contacts, reports and reminders, and a loader that puts them into the app.
- `tests/TEST_CASES.md` has the manual test cases (functional, security, accessibility, offline).

Load sample data:

1. Open the app in Chrome, then DevTools, then Console.
2. Paste the contents of `sample-data/load-sample-data.js` and press Enter.
3. Reload the page.

## Documentation

- [Technical Design Document](docs/TECHNICAL_DESIGN.md): architecture, data flow, storage, security, diagrams

## Data and privacy

All personal data (profile, contacts, reports, reminders, chats) is stored only in the browser on your device. The app contacts these third-party services when the matching feature is used: Google Translate (text to translate), Open-Meteo (weather for your location), Google Fonts, YouTube and OpenStreetMap links. Government links open official websites.

## Deployment

Static hosting works: GitHub Pages, Netlify, Vercel, Cloudflare Pages or any web server over HTTPS. Upload `index.html`, `manifest.webmanifest`, `sw.js` and icons.

## Contributing

Issues and pull requests are welcome. Please test with `tests/TEST_CASES.md` before submitting.

## License

MIT. See [LICENSE](LICENSE).

## Author

Kaviya S
