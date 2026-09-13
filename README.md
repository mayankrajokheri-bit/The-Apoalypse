# The-Apoalypse
# 🎃 The Apocalypse: Reality Quest AI

> *Your camera is your weapon. Your city is your dungeon.*

**The Apocalypse** (a.k.a. **Reality Quest AI**) is a location-based, AI-powered AR game that turns real-world objects into RPG items. Point your phone's camera at a tree, a laptop, or a water bottle, and a multimodal AI "transmutes" it into a magical weapon, potion, or resource — while a 7-level horror storyline set at **GMN College, Ambala Cantt** unfolds around you.

This repository is a bundle built during a hackathon and contains the main game plus a couple of standalone mini-games created alongside it.

---

## 📦 What's in this repo

| Folder | What it is |
|---|---|
| `reality-quest-ai-clean/` | **Main project.** The AR/location game — Capacitor-based mobile app + web prototype. Start here. |
| `reality-quest-ai/` | Same project as above, plus local build artifacts (`node_modules/`, a zipped copy, Gradle cache). Kept for reference; not needed to run the game. |
| `Game-Bundle-All/` | A combined bundle folder containing copies of the game + the mini-games below (looks like an export used for a single hackathon submission). |
| `subway-surfers/` | Standalone "Subway Surfers — 3D Cyber Run" clone built with Three.js. |
| `The-Apoalypse-Game/`, root `index.html` / `script.js` / `style.css` | A standalone "Neon Tic-Tac-Toe" mini-game (2-player + unbeatable Minimax AI). |

> ⚠️ **Note on duplication:** `reality-quest-ai` and `reality-quest-ai-clean` are nearly identical, and `Game-Bundle-All` duplicates the other folders again. If you're publishing this to GitHub, consider keeping only `reality-quest-ai-clean/` (the game) and one copy of each mini-game, and adding a `.gitignore` for `node_modules/`, `android/.gradle/`, and `*.zip` to shrink the repo significantly (the raw folder is ~290MB, mostly build cache and a redundant zip).

---

## 🎮 Main Game: The Apocalypse — Reality Quest AI

### Story
An ancient grimoire opens, revealing a cursed map of Haryana, India. Ten engineering students must infiltrate **GMN College** and survive **7 deadly trials** — from *The Locked Gate* (Level 1) to *The Final Battle* (Level 7) — while an AI transmutes the real world into the tools they need to survive.

### Core gameplay loop
1. **Detect location** — GPS pinpoints the player and generates nearby points of interest and weather-based quests.
2. **Scan** — Point the in-app camera at a real object and capture a frame.
3. **AI transmutation** — The frame is sent to a multimodal vision model, which classifies the object and returns a structured RPG item (name, rarity, stats, lore, XP/coin rewards).
4. **Progress** — Collected items complete quests, grant XP, and unlock new map sectors/levels.

Example transmutations:
- 🌲 Tree → Magical Sylvan Wood (crafting resource)
- 💧 Water bottle → Starlight Health Potion
- 🪑 Chair → Aegis Kinetic Shield
- 💻 Laptop → Quantum Cyber Blade
- 🐕 Dog → Solar Companion Familiar

### Cast — The 10 Survivors of GMN College
Each survivor has an engineering major, a role, and a gameplay perk (e.g. Aarav — Robotics & AI, Lead Scout, +20% sprint speed & radar; Ben — Electrical Eng, fast circuit decryption). See `www/js/survivors.js` for the full roster.

### Tech stack
- **Frontend:** HTML5 / CSS3 / vanilla JavaScript, packaged as a mobile app with [Capacitor](https://capacitorjs.com/) (Android)
- **Vision AI:** Google Gemini 1.5 Flash (multimodal image classification), with an offline keyword-based fallback engine (`js/aiEngine.js`) so the game still works without an API key
- **Maps:** Custom cyberpunk vector map with radial node spawns; Leaflet/Google Maps referenced in the architecture docs
- **Planned backend (per docs):** Firebase Authentication, Cloud Firestore, Cloud Storage, and Cloud Functions for real-time sync and anti-cheat
- **Alternate client:** an Expo/React Native starter is included at `reality-quest-ai-clean/react-native-starter/`

Full system diagrams, the Firestore schema, and the Gemini prompt/JSON contract are documented in [`reality-quest-ai-clean/docs/ARCHITECTURE.md`](reality-quest-ai-clean/docs/ARCHITECTURE.md). A hackathon pitch deck and 2-minute demo script live in [`reality-quest-ai-clean/docs/HACKATHON_PITCH.md`](reality-quest-ai-clean/docs/HACKATHON_PITCH.md).

### Project structure (`reality-quest-ai-clean/`)
```
reality-quest-ai-clean/
├── index.html, level1.html … level7.html   # Level pages
├── gate.html, splash.html, hackathon.html  # Intro / splash / pitch screens
├── css/                                    # Stylesheets
├── js/                                     # App logic, AI engine, map, state, sound
├── assets/                                 # Images, sprites, level art
├── www/                                    # Capacitor web bundle (mirrors the app for build)
├── android/                                # Android (Capacitor) native project
├── react-native-starter/                   # Alternate Expo/React Native client
├── scripts/                                # PowerShell asset-processing scripts
├── docs/                                   # Architecture & pitch documentation
├── capacitor.config.json
├── build_apk.bat                           # One-click Android debug APK build (Windows)
├── server.js
└── package.json
```

### Running the web prototype
No build step is required for the browser version:
```bash
cd reality-quest-ai-clean
npm install
npm start          # runs server.js
```
Then open the app in your browser (check `server.js` for the port), or simply open `index.html` directly for a static preview.

### Building the Android app
```bash
cd reality-quest-ai-clean
npx cap sync android
build_apk.bat        # Windows helper: builds a debug APK via Gradle
```
The resulting APK is placed at `android/app/build/outputs/apk/debug/app-debug.apk`.

---

## 🕹️ Bonus mini-games

### Neon Tic-Tac-Toe
A polished tic-tac-toe game with 2-player and single-player (unbeatable Minimax AI) modes, XP/level HUD, and neon glassmorphism styling.
```bash
cd The-Apoalypse-Game   # or open the root index.html directly
# open index.html in a browser
```

### Subway Surfers — 3D Cyber Run
A Three.js-powered endless-runner clone: dodge trains, jump hurdles, and surf on hoverboards.
```bash
cd subway-surfers
# open index.html in a browser (loads Three.js from a CDN)
```

---

## 🛠️ Requirements
- A modern browser for the web prototypes (camera/geolocation permissions needed for the AR scanner)
- Node.js + npm for the Capacitor build pipeline
- Android Studio / Gradle for building the native Android app
- (Optional) A Google Gemini API key to enable live AI vision classification — without one, the game falls back to its built-in keyword-matching engine

## 📄 License
No license file is currently included. Add a `LICENSE` file if you intend to open-source this project publicly.

## 🙏 Credits
Built for a hackathon under the theme **"Real World × AI × Gaming."** Setting inspired by GMN College, Ambala Cantt, India.
