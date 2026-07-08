<div align="center">

# 🏥 PHC Smart Manager

**A smart dashboard for tracking medical supplies, inventory, and staff attendance at rural Primary Health Centres (PHCs).**

[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=white)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Built%20with-Vite-646CFF?logo=vite&logoColor=white)](https://vitejs.dev/)
[![Gemini API](https://img.shields.io/badge/AI-Gemini-8E75B2?logo=google&logoColor=white)](https://ai.google.dev/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Open Issues](https://img.shields.io/github/issues/samikshakalra02/PHC-Smart-Manager)](https://github.com/samikshakalra02/PHC-Smart-Manager/issues)
[![Last Commit](https://img.shields.io/github/last-commit/samikshakalra02/PHC-Smart-Manager)](https://github.com/samikshakalra02/PHC-Smart-Manager/commits/main)

[Features](#-features) •
[Tech Stack](#-tech-stack) •
[Project Structure](#-project-structure) •
[Getting Started](#-getting-started) •
[Usage](#-usage) •
[Roadmap](#-roadmap) •
[Contributing](#-contributing)

</div>

---

## 📖 Table of Contents

- [About](#-about)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Environment Variables](#environment-variables)
  - [Running the App](#running-the-app)
  - [Building for Production](#building-for-production)
- [Usage](#-usage)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [License](#-license)
- [Contact](#-contact)

---

## 🩺 About

**PHC Smart Manager** replaces paper registers at rural Primary Health Centres with a single live dashboard. Frontline staff log updates in plain language — in English or a regional Indian language — and Gemini turns that free text into structured, trackable data, so health officers always know what's in stock and who's on duty without waiting for a monthly report.

## ✨ Features

| Feature | Description |
|---|---|
| 📊 **Dashboard Overview** | Real-time tracking of medicine quantities (e.g. Paracetamol, Anti-Venom) |
| 👩‍⚕️ **Staff Attendance** | Live view of active medical officer rosters, by shift |
| 🧮 **Regional Supply Grid** | A cross-PHC matrix view highlighting low-stock and critical-deficit centres |
| 🤖 **AI Report Parser** | Gemini turns conversational field notes — in English, Hindi, Bengali, Marathi, Telugu, Tamil, Gujarati, Kannada, Malayalam, or Punjabi — into structured inventory & attendance updates |
| 🌐 **Multi-language UI** | Full interface translation across 10 Indian languages, with an on-demand Gemini translation endpoint |
| 🔊 **Audio & Simple Mode** | Text-to-speech playback and a large-button, simplified layout for low-literacy or low-connectivity use |
| 🗺️ **Smart Maps** | Google Maps view of PHC locations, with a fallback to the Mangaluru hub if the browser blocks geolocation |
| 📜 **Activity Log** | A running feed of inventory, attendance, and system events across centres |

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 19, TypeScript, Vite 6 |
| Styling | Tailwind CSS 4 |
| Animation | Motion (Framer Motion) |
| Icons | lucide-react |
| Maps | `@vis.gl/react-google-maps` (Google Maps Platform) |
| Backend | Node.js, Express |
| AI | Google Gemini API (`@google/genai`) — report parsing & translation |
| Build | Vite (client) + esbuild (server bundle) |

## 📁 Project Structure

```
PHC-Smart-Manager/
├── .env.example              # Sample environment variables (copy to .env)
├── index.html                 # Vite entry HTML
├── metadata.json               # App metadata (AI Studio frame permissions, capabilities)
├── package.json                 # Dependencies & scripts
├── server.ts                     # Express server: /api/extract-logistics, /api/translate
├── tsconfig.json                   # TypeScript configuration
├── vite.config.ts                   # Vite build configuration
├── LICENSE
├── README.md
└── src/
    ├── main.tsx               # React entry point
    ├── App.tsx                 # Root component: layout, view routing, shared state
    ├── index.css                # Tailwind entry & global styles
    ├── types.ts                   # Shared TypeScript interfaces
    ├── data.ts                     # Seed/mock data for inventory, doctors, matrix, events
    ├── components/
    │   ├── DashboardView.tsx    # Inventory overview & AI report parser
    │   ├── AttendanceView.tsx    # Staff roster & shift tracking
    │   ├── MatrixView.tsx         # Regional multi-PHC supply grid
    │   ├── MapView.tsx             # Google Maps PHC locator
    │   └── UpdatesView.tsx           # Activity / event log
    └── utils/
        ├── translations.ts         # UI string translations (10 languages)
        ├── attendanceTranslations.ts # Attendance-specific translations
        └── audio.ts                  # Text-to-speech helpers
```

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18 or later
- A [Google Gemini API key](https://ai.google.dev/)
- A [Google Maps Platform API key](https://console.cloud.google.com/google/maps-apis) (for the map view)

### Installation

```bash
# Clone the repository
git clone https://github.com/samikshakalra02/PHC-Smart-Manager.git
cd PHC-Smart-Manager

# Install dependencies
npm install
```

### Environment Variables

Copy the example file and add your credentials:

```bash
cp .env.example .env
```

| Variable | Description |
|---|---|
| `GEMINI_API_KEY` | Server-side Gemini key, used to parse field notes and translate text |
| `GOOGLE_MAPS_PLATFORM_KEY` | Client-side Google Maps Platform key, used by the map view |

### Running the App

```bash
npm run dev
```

This starts the Express server (`server.ts`) with Vite in middleware mode. The app will be available at `http://localhost:3000`.

### Building for Production

```bash
npm run build   # Builds the client with Vite and bundles the server with esbuild
npm run start   # Runs the production bundle from dist/server.cjs
```

## 📋 Usage

1. Log in as PHC staff and enter a plain-language update (e.g. *"Used 12 ORS packets, doctor is present"*), in English or a regional language.
2. The AI Report Parser (`/api/extract-logistics`) converts it into structured inventory and attendance data.
3. View live stock levels, staff rosters, the regional supply grid, and centre locations on the dashboard.
4. Switch the UI language at any time; free-text content can also be translated on demand via `/api/translate`.
5. Health officers can monitor multiple centres from a single view.

## 🗺 Roadmap

- [ ] Add automated tests for the AI report parser
- [ ] Add authentication & role-based access (staff vs. officer)
- [ ] Persist inventory/attendance data (currently seeded from `src/data.ts` in memory)
- [ ] Low-stock alerts & notifications
- [ ] CI pipeline (lint + type-check on PRs)

## 🤝 Contributing

Contributions are welcome!

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m 'Add some feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

Before opening a PR, please run `npm run lint` (type-checks the project with `tsc --noEmit`).

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

## 📬 Contact

**Samiksha Kalra** — [GitHub](https://github.com/samikshakalra02)

Project Link: [https://github.com/samikshakalra02/PHC-Smart-Manager](https://github.com/samikshakalra02/PHC-Smart-Manager)
