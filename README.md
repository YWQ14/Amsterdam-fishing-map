# Amsterdam Fishing Intelligence Map (2024–2026)

Interactive fishing map, spot discovery platform, algorithmic ranking engine, and community catch & regulations database covering Amsterdam and surrounding waterways.

## Architecture & Component Separation

```text
amsterdam-fishing-map/
├── src/
│   ├── index.html                   # Main multi-view dashboard application shell
│   ├── data/
│   │   ├── fishing_spots.json       # Structured database of 27 researched locations & coordinates
│   │   ├── catch_reports.json       # Documented 2025–2026 catch reports (separating catchDate vs publicationDate)
│   │   ├── regulations.json         # Official AHV, VISpas, VISplanner & Waterschap AGV rules
│   │   └── sources.json             # 22 traceable official, federation, specialist & community sources
│   ├── engine/
│   │   └── ranking_algorithm.js     # Transparent 7-factor weighted scoring & confidence engine
│   └── frontend/
│       ├── styles.css               # Dark-themed responsive outdoor mapping interface
│       └── app.js                   # Leaflet map controller, clustering, filters & modals
├── dist/
│   └── Amsterdam_Fishing_Intelligence_Map.html  # Self-contained compiled application bundle
├── server.ps1                       # Local HTTP & REST API server (GET/POST /api/spots, /api/catches)
├── build.ps1                        # Compiler that packages src/ into dist/
└── validate_and_test.ps1            # Automated data validation and ranking verification script
```

## How to Run the Application

### Option A: Zero-Install Standalone Browser Mode (Fastest)
Open **`dist\Amsterdam_Fishing_Intelligence_Map.html`** directly in **Microsoft Edge**, **Google Chrome**, or **Firefox**.
- All 27 locations, 12 documented catch reports, regulations, and 22 research sources are pre-loaded.
- New spots and catch reports added via the UI are persisted in `localStorage` and can be exported at any time via **⬇ Export DB**.

### Option B: Local REST API Server Mode (Full Disk Persistence)
Run the included PowerShell HTTP & REST API server:
```powershell
cd C:\Users\pnl0p86y\.gemini\antigravity\scratch\amsterdam-fishing-map
.\server.ps1 -Port 8080
```
Then open **`http://localhost:8080`** in your browser.
- Adding a new spot (**`+ Add Spot`**) or catch report (**`+ Log Catch Report`**) writes directly to `src/data/fishing_spots.json` and `src/data/catch_reports.json`.
- After updating `src/data/*.json`, run `.\build.ps1` to regenerate `dist\Amsterdam_Fishing_Intelligence_Map.html`.

