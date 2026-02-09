# CallGlass
CallGlass — Real‑Time Ham Radio Callsign Listener & Dashboard
CallGlass is a full Windows‑integrated ham‑radio monitoring suite that:

Listens to live audio from your radio or microphone

Detects ham radio callsigns using Whisper speech recognition

Computes signal strength and confidence scoring

Logs everything into SQLite

Streams real‑time data to a modern React + Tailwind dashboard


Includes a Windows desktop GUI with:

Start/Stop backend + dashboard

Auto‑start option

System tray icon showing CPU usage

Live callsign display

Recent callsign table

Everything runs with one click from the GUI.

Features
🎙️ Audio Processing
Real‑time audio capture (sounddevice)

Whisper.cpp  transcription

Callsign extraction via regex

Confidence scoring (STT confidence + repeats + signal strength)

📡 Backend (FastAPI)
REST API for logs

WebSocket for live updates

Background worker for audio + detection

SQLite database

🖥️ Windows Desktop App (PyQt6)
Start/Stop backend and dashboard

Auto‑start on launch

System tray with CPU usage indicator

Live callsign info

Recent callsign table

Opens dashboard in browser

🌐 Web Dashboard (React + Tailwind)
Real‑time callsign display

Recent callsign table

Clean, modern UI

Auto‑refresh via WebSocket
<img width="475" height="701" alt="Screenshot 2026-02-09 090314" src="https://github.com/user-attachments/assets/7029d7ab-d1d2-4bfe-bacb-7f80987abcc4" />

Project Structure
Code
callglass/
│
├── backend/
│   ├── main.py
│   ├── config.py
│   ├── worker.py
│   │
│   ├── audio/
│   │   ├── listener.py
│   │   ├── signal_strength.py
│   │   └── whisper_engine.py
│   │
│   ├── detection/
│   │   ├── callsign_parser.py
│   │   └── confidence.py
│   │
│   ├── db/
│   │   ├── database.py
│   │   └── models.py
│   │
│   └── routers/
│       ├── callsigns.py
│       └── live.py
│
├── desktop/
│   ├── app.py
│   ├── tray.py
│   ├── server.py
│   ├── dashboard_server.py
│   ├── ws_client.py
│   └── config.json
│
├── dashboard/
│   ├── package.json
│   ├── postcss.config.cjs
│   ├── tailwind.config.cjs
│   ├── vite.config.mts
│   └── src/
│       ├── main.jsx
│       ├── App.jsx
│       ├── websocket.js
│       ├── index.css
│       │
│       ├── pages/
│       │   └── Home.jsx
│       │
│       └── components/
│           ├── LatestCard.jsx
│           └── CallsignTable.jsx
│
└── README.md
Installation
1. Install Python dependencies
From the project root:

bash
pip install fastapi uvicorn sqlalchemy pydantic python-multipart
pip install sounddevice numpy whispercpp
pip install PyQt6 psutil websocket-client requests
pip install aiosqlite
2. Install Node.js (for dashboard)
Download from:
https://nodejs.org

Verify:

bash
node -v
npm -v
3. Install dashboard dependencies
bash
cd callglass/dashboard
npm install
Running CallGlass
Option A — Recommended: Use the Windows GUI
From project root:

bash
python desktop/app.py
In the GUI:

Click Start Backend + Dashboard

Dashboard opens at:
http://localhost:5173

The GUI will:

Launch backend (FastAPI + worker)

Launch dashboard (Vite dev server)

Show CPU usage in tray

Display live callsign info

Log callsigns to SQLite

Option B — Run backend manually
bash
uvicorn backend.main:app --host 0.0.0.0 --port 8000
Option C — Run dashboard manually
bash
cd dashboard
npm run dev
Configuration
desktop/config.json
json
{
  "auto_start": false
}
Set "auto_start": true to automatically launch backend + dashboard when the GUI opens.

How It Works
Audio Pipeline
Audio captured via sounddevice

Whisper.cpp  transcribes PCM frames

Callsign regex extracts valid calls

Confidence engine scores each detection

SQLite logs high‑confidence calls

Backend
FastAPI serves REST + WebSocket

Worker thread runs audio loop

Dashboard and GUI subscribe to live feed

Dashboard
React + Tailwind

WebSocket for real‑time updates

Displays newest call + recent table

Desktop App
Controls backend + dashboard

Shows live callsign info

Minimizes to tray

Displays CPU usage

License
MIT License (or whatever you choose)

Author
Joshua (your GitHub username here)
