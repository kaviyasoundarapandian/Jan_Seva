# Jan Seva (जन सेवा)

> **सेवा सबकी, अधिकार सबका** — Service for all, rights for all.

Jan Seva is a free, privacy-first citizen-services app for India. It brings emergency help, civic complaints, disaster alerts, health tools, government schemes, documents, legal rights, payments, travel and learning into **one app**, in **22 Indian languages**. No sign-up is needed: you can use everything as a guest, and anything you save stays **on your phone**.

It ships as a single web app (`index.html`) that runs in the browser and is packaged as an Android app (WebView) for the Play Store / APK install.

---

## Features

| Area | What you can do |
|---|---|
| **Emergency** | One-tap calls to 112 / 108 / 100 / 101, Women's Safety **SOS** that SMSes your live location to saved contacts, first-aid help |
| **Report a problem** | Report dustbins, drains, toilets, potholes, mosquito water, street cleaning, corruption and more; add a photo and GPS location; report anonymously; track status and rate the response |
| **Disaster** | Early warning for your location (weather/forecast), auto-alert option, guides for flood, cyclone, earthquake, fire, landslide, tsunami; rescue-message helper |
| **Necessity** | Find water points, hospitals, toilets, pharmacies, ATMs, banks, police and more near you |
| **Transport & routes** | Route planner (walk / drive / transit), train, flight and bus lookups, metro links |
| **Health & care** | Step counter, heart-rate log, water and meal tracker, medicine/vaccination reminders, auto-emergency-call on fall detection |
| **Govt schemes** | Scheme finder by state, farmer box, scholarships, official portals |
| **Old age persons** | Pension tracker (type, amount, due day, received months) |
| **News & radio** | City news, epapers, live radio |
| **Pay & bills** | Trusted payment apps, electricity / water / gas bills, FASTag, scam-safety tips |
| **Savings & investing** | Income split (needs / wants / savings), savings goals |
| **Govt documents & ID** | Aadhaar, PAN, passport, voter ID, driving licence, appointments — official links only |
| **Legal help & rights** | Free legal aid (NALSA 15100), labour and food rights by state, consumer, tenant and cyber-crime help |
| **Govt exams & jobs** | Exams matched to your qualification, exam reminders |
| **Blood donation** | Donor registration and blood-request helpers |
| **Agriculture & water** | Farmer tools, mandi prices, water and soil links |
| **Translator** | Speak or type, translate across Indian languages, listen to the result |
| **Accessibility / Divyang learning** | Voice input, text-to-speech, sign-language recognition (on-device model), learning tools |
| **Nanba (friend)** | A caring chat companion for questions, worries and encouragement |
| **Find anything** | Search across all tabs and features from the home screen |
| **Security** | Optional profile with PIN / password (PBKDF2 + salted hash, stored locally) |

## Supported languages

English, Hindi, Assamese, Bengali, Bodo, Dogri, Gujarati, Kannada, Kashmiri, Konkani, Maithili, Malayalam, Manipuri, Marathi, Nepali, Odia, Punjabi, Sanskrit, Santali, Sindhi, Tamil, Telugu, Urdu.

## Privacy

- No account, no server, no analytics. Profile, reports, contacts, places, health data and reminders are stored in the device's `localStorage` (keys prefixed `ns_`).
- Location, camera, microphone and notifications are requested **only when you use a feature that needs them**.
- Official links open the original government websites. Jan Seva does not collect OTPs, PINs or card numbers.
- Jan Seva is **not** an official government app. Verify details on the linked official site.

## Project structure

```
Jan_Seva/
├── index.html              # The whole app (HTML + CSS + JS, single file)
├── load-sample-data.js     # Seeds demo data for testing / screenshots / demo video
├── README.md
├── TECHNICAL_DESIGN.md     # Architecture, data model, security, build
├── TEST_CASES.md           # Manual + smoke test cases
└── LICENSE                 # MIT
```

The Android package wraps `index.html` in a WebView (assets: `index.html`, `model.json`, `metadata.json`).

## Run locally

```bash
# any static server works
python3 -m http.server 8000
# open http://localhost:8000/index.html
```

Opening `index.html` directly also works for most features. Geolocation, camera, microphone and the service worker need `https://` or `localhost`.

### Load demo data

1. Open the app, tap **Continue as guest** (or create a profile).
2. Open the browser console (DevTools) and paste the contents of `load-sample-data.js`, or add `<script src="load-sample-data.js"></script>` temporarily.
3. Reload the page. To remove the demo data run `JanSevaSample.clear()` in the console.

## Build the Android app

1. Create an Android Studio project (Empty Views Activity, Kotlin).
2. Copy `index.html`, `model.json`, `metadata.json` into `app/src/main/assets/`.
3. Load the page through `WebViewAssetLoader` (`https://appassets.androidplatform.net/assets/index.html`) with JavaScript, DOM storage and geolocation enabled.
4. Declare permissions: `INTERNET`, `ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION`, `CAMERA`, `RECORD_AUDIO`, `POST_NOTIFICATIONS`.
5. Build a signed APK / AAB.

## Emergency numbers used

| Number | Service |
|---|---|
| 112 | Police, fire, ambulance (all India) |
| 108 | Ambulance |
| 100 | Police |
| 101 | Fire |
| 1098 | Child helpline |
| 1091 / 181 | Women helpline |
| 15100 | Free legal aid (NALSA) |

## Contributing

Issues and pull requests are welcome. Please keep the app a single self-contained file, keep every user-facing string translatable, and do not add trackers or third-party analytics.

## License

[MIT](LICENSE) © 2026 Kaviya S
