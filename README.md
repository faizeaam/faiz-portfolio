# Faiz E Aam Ansari - Portfolio and Projects

This repository contains my personal portfolio website, browser-based projects, games, and IGNOU BCA Semester 1 Study Lab. The projects are built mainly with HTML, CSS, and vanilla JavaScript, with selected services used for maps, weather data, and optional real-time messaging.

## Contents

- [Portfolio](#portfolio)
- [Projects](#projects)
- [Technology](#technology)
- [Run Locally](#run-locally)
- [Hosting](#hosting)
- [Gather Messages Setup](#gather-messages-setup)
- [Privacy and Security](#privacy-and-security)
- [Repository Layout](#repository-layout)
- [Credits and Licenses](#credits-and-licenses)
- [Owner and Contact](#owner-and-contact)

## Portfolio

`index.html` is the portfolio home page. It introduces the owner and links to selected work, browser games, the Study Lab, the About section, and contact profiles. The page is responsive and includes project cards, a game gallery, a short skills section, and links to the individual demos.

## Projects

| File | Project | Description |
| --- | --- | --- |
| `student-task-manager.html` | Student Task Manager | Add, complete, filter, and save study tasks in the browser. |
| `weather-app.html` | Weather Dashboard | Look up a city and see current conditions and a five-day forecast. Uses Open-Meteo geocoding and forecast APIs. |
| `expense-tracker.html` | Paisa Expense Tracker | Record income and expenses, organize transactions, and view the current balance. Data is stored locally in the browser. |
| `locateme.html` | LocateMe | Request the visitor's browser location and display it on a map. Location access requires permission. |
| `quiz-app.html` | CodeSprint Quiz | Answer frontend questions, see feedback and score, and restart the quiz. |
| `studyhub.html` | StudyHub Dashboard | Student workspace with tasks, notes, a focus timer, and progress tracking. |
| `car-game.html` | Traffic Rush | Canvas driving game with keyboard controls, scoring, and a locally saved best score. |
| `notes-app.html` | Quick Notes | Create and manage notes saved in browser storage. |
| `messaging-app.html` | Gather Messages | Chat UI with a local demo mode and optional Firebase accounts, Firestore messaging, and Olm end-to-end encryption. |
| `memory-match.html` | Memory Match | Card-matching game with a locally saved best score. |
| `tic-tac-toe.html` | Tic Tac Toe | Two-player browser version of the classic game. |
| `whack-a-mole.html` | Whack-a-Mole | Timed reaction game. |
| `snake-game.html` | Snake | Keyboard-controlled snake game. |
| `pong-game.html` | Pong | Canvas paddle game against the CPU. |
| `space-shooter.html` | Space Shooter | Canvas arcade game where the player shoots incoming enemies. |
| `study-lab.html` | Study Lab | IGNOU BCA Semester 1 question papers, assignments, and study material. |

### Study Lab

The Study Lab separates previous-year question papers, assignments, and books/study PDFs. Question papers can be filtered by subject and year and searched by course/session. Study material can be filtered by subject code, block, and unit, or searched by code/title. The current book list contains 75 entries.

Study material links point to public IGNOU eGyanKosh files or course collections. The PDFs are not copied into this repository, which keeps the repository smaller and uses the official source. Some courses or units may not have a separate direct PDF available in the repository.

Question paper links refer to the official IGNOU archive. The page maps legacy course codes where applicable, including BCS-011 to BCS-111 and FEG-2 to FEG-02.

## Technology

- HTML5, CSS3, and vanilla JavaScript; there is no frontend framework or application build step.
- Responsive layouts and semantic page structure across the portfolio and demos.
- Browser `localStorage` for local tasks, notes, scores, demo chats, and other project data.
- Fetch API for Open-Meteo weather and geocoding requests.
- Geolocation API and Leaflet 1.9.4 with OpenStreetMap tiles for LocateMe.
- Canvas API for selected games.
- Firebase Authentication and Cloud Firestore for optional live Gather Messages.
- Matrix Olm Double Ratchet for live-message encryption in Gather Messages.

Some pages load fonts, maps, Firebase modules, weather data, or other resources from external services and therefore need an internet connection for those features.

## Run Locally

Most standalone pages can be opened directly in a browser. For a consistent local website origin, use VS Code Live Server:

1. Open this repository folder in VS Code.
2. Start Live Server from `index.html` or another project page.
3. Use the links on the portfolio or open a specific HTML file.

Live Server or HTTPS is required for browser modules and is recommended for APIs and geolocation. The real-time Firebase chat does not connect when opened using a `file://` URL; outside Firebase Hosting it runs in local demo mode.

### Rebuild the Olm Bundle

Node.js and npm are only needed when changing the encryption source and rebuilding its browser bundle:

```sh
npm install
npm run build:crypto
```

The build uses `esbuild` and writes `olm-e2ee.bundle.js`. The Olm WebAssembly runtime is provided by `olm.wasm`.

## Hosting

### Portfolio and Project Pages

The repository-root `index.html` is the portfolio entry point. To publish the portfolio and project pages with GitHub Pages, configure Pages to serve the repository root (or the branch/folder where these root files are published). Keep linked HTML files beside `index.html` so relative project links continue to work.

The Study Lab page is the root `study-lab.html`. Its course PDFs are linked from eGyanKosh and are not uploaded with this repository.

### Firebase Hosting for Gather Messages

`firebase.json` sets the Firebase Hosting public directory to `hosting/`. That folder contains the Gather Messages hosting entry point and its required chat files; it is separate from the root portfolio site. The Firebase project alias is in `.firebaserc`.

Using Firebase Hosting requires the Firebase CLI and a Firebase account with access to the configured project. Configure Authentication and Firestore as described below before enabling live chats.

## Gather Messages Setup

The local demo works without a Firebase connection. To use real accounts and cross-device conversations on Firebase Hosting:

1. Create or select a Firebase project and register a Web app.
2. Enable Email/Password in Firebase Authentication.
3. Create a Cloud Firestore database.
4. Set the Web app configuration in `firebase-config.js` and its matching copy under `hosting/` if those files are deployed separately.
5. Publish `firestore.rules` to the project's Firestore Rules.
6. Deploy the `hosting/` directory with Firebase Hosting and open the site over HTTPS.
7. Create accounts, share account IDs directly with friends, start a chat, and compare safety numbers through a trusted channel before verifying the contact.

The Firebase Web app configuration in a static client is public by design. Never place a Firebase service-account key or other server secret in this repository.

## Privacy and Security

- Local project data such as tasks, notes, expenses, and game scores stays in the browser's storage for that site origin. Clearing browser/site data can remove it.
- LocateMe requests browser geolocation permission to show the visitor's own position on a map. It does not track other people or phone numbers.
- In live Gather Messages, Firestore stores encrypted message payloads plus the metadata needed to deliver and display conversations. Users must verify a matching safety number before live messages are sent or decrypted.
- Olm identity keys are stored in browser IndexedDB and are not backed up. The current implementation is single-device per account; clearing site data or switching devices can make that device's encrypted history unavailable.
- Messages created before end-to-end encryption was introduced remain unencrypted and are identified as such in the app.
- This is a client-side project: a site owner who can change the hosted JavaScript could change how the application behaves. Do not rely on the hosted app alone for highly sensitive communication.

## Repository Layout

```text
index.html                 Portfolio home page
assets/student-task-manager.png  Student Task Manager card preview
study-lab.html             Question papers, assignments, and book links
student-task-manager.html  Student task manager
weather-app.html           Weather dashboard
expense-tracker.html       Expense tracker
locateme.html              Location and map demo
quiz-app.html              CodeSprint quiz
studyhub.html              StudyHub dashboard
notes-app.html             Quick Notes
messaging-app.html         Gather Messages entry point
car-game.html              Traffic Rush
memory-match.html          Memory Match
tic-tac-toe.html           Tic Tac Toe
whack-a-mole.html          Whack-a-Mole
snake-game.html            Snake
pong-game.html             Pong
space-shooter.html         Space Shooter
firebase-chat.js           Firebase Auth and Firestore client
firebase-config.js         Public Firebase Web app configuration
olm-e2ee.js                Olm encryption source
olm-e2ee.bundle.js         Browser bundle
olm.wasm                   Olm WebAssembly runtime
firestore.rules            Firestore security rules
hosting/                   Firebase Hosting copy of Gather Messages files
package.json               Olm bundle build script and dependencies
package-lock.json          Locked npm dependency versions
README.md                  Project documentation
THIRD-PARTY-NOTICES.md     Third-party notices
LICENSE-APACHE-2.0.txt     Olm license text
```

`node_modules/`, Firebase local cache files, and logs are excluded by `.gitignore`.

## Credits and Licenses

- Gather Messages uses `@matrix-org/olm` 3.2.15, distributed under Apache License 2.0. See [LICENSE-APACHE-2.0.txt](LICENSE-APACHE-2.0.txt) and [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).
- LocateMe uses Leaflet and OpenStreetMap tiles and includes OpenStreetMap attribution in the app.
- Weather data and city search use Open-Meteo APIs.
- Portfolio imagery and fonts may be loaded from Unsplash and Google Fonts.
- Study Lab course material links lead to the IGNOU eGyanKosh repository; question-paper links lead to IGNOU's archive.

The Apache license file here documents the bundled Olm component; it does not by itself declare a license for every project in this repository.

## Owner and Contact

**Faiz E Aam Ansari**  
IGNOU BCA student and frontend developer focused on responsive interfaces and practical web applications.

- Email: [faizz9165326@gmail.com](mailto:faizz9165326@gmail.com)
- GitHub: [github.com/faizeaam](https://github.com/faizeaam)
- LinkedIn: [linkedin.com/in/faiz-e-aam-ansari](https://www.linkedin.com/in/faiz-e-aam-ansari)

The portfolio lists the owner as available for internships.
