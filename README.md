<div align="center">

# ⛏️ TerraMesh AI (MineGuard)
### AI-Powered Mine Subsidence Early Warning & Safety Command Center

**Continuous, multi-sensor geotechnical monitoring and AI hazard prediction for underground coal mines**  
*Developed for Smart India Hackathon 2026 · Problem Statement SIH26025 (Ministry of Coal / Coal India Limited)*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.11+](https://img.shields.io/badge/Python-3.11+-3776AB.svg?logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-009688.svg?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![React 19](https://img.shields.io/badge/React-19-61DAFB.svg?logo=react&logoColor=black)](https://react.dev/)
[![Expo](https://img.shields.io/badge/Expo-SDK_57-000020.svg?logo=expo&logoColor=white)](https://expo.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-6.0-3178C6.svg?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-TimescaleDB-336791.svg?logo=postgresql&logoColor=white)](https://www.timescale.com/)
[![Redis](https://img.shields.io/badge/Redis-7.0+-DC382D.svg?logo=redis&logoColor=white)](https://redis.io/)
[![MQTT](https://img.shields.io/badge/MQTT-Mosquitto-660066.svg?logo=eclipsemosquitto&logoColor=white)](https://mosquitto.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-Risk_Engine-2E7D32.svg)](https://xgboost.readthedocs.io/)

</div>

---

## 📌 Overview

Underground coal mining in complex geological strata is vulnerable to **mine subsidence** and sudden roof falls. Traditional surveillance methods — manual rod surveys, dial gauges, or periodic satellite InSAR passes — are either too infrequent, cost-prohibitive, or unable to provide immediate tactical warnings to evacuation teams.

**TerraMesh AI** is an end-to-end mine subsidence monitoring, predictive hazard analysis, and emergency evacuation platform. It integrates:
1. **IoT Edge Telemetry**: Multi-parameter sensing covering tilt, displacement velocity, crack expansion, pore pressure, microseismic vibration, and hazardous gas concentrations (CH₄, CO).
2. **Edge Hardware-in-the-Loop Contract**: Validated 35-check contract for sensor packet sanity, range boundaries, and fail-safe degraded modes.
3. **Multi-Model AI Hazard Engine**: Dual-engine pipeline featuring an 18-feature XGBoost risk classifier and an Isolation Forest multivariate anomaly detector.
4. **Interactive 3D Digital Mine Twin**: Real-time WebGL scene built on Three.js rendering underground shafts, galleries, fault lines, deformation strain cones, and live sensor beacons.
5. **GIS Geospatial Command Center**: Leaflet GIS map with dynamic zoning, worker tracking, biometric status, and A* evacuation corridors.
6. **Multilingual Mobile Worker App**: Cross-platform Expo/React Native companion application with real-time WebSocket telemetry, panic alerts, and full localization in 5 Indian languages.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          TerraMesh AI — System Architecture                 │
├─────────────────┬─────────────────────────────┬─────────────────────────────┤
│   EDGE & IOT    │     BACKEND & CLOUD         │       USER INTERFACES       │
│                 │                             │                             │
│ • ESP32 / Nodes │ • FastAPI REST & WebSocket  │ • React 19 Web Dashboard    │
│ • LoRa Mesh     │ • TimescaleDB (Hypertables) │ • Three.js 3D Digital Twin  │
│ • Microseismic  │ • PostGIS Spatial Layers    │ • Leaflet GIS Risk Map      │
│ • MQTT Broker   │ • Redis 7 In-Memory Cache   │ • Expo/React Native Mobile  │
│ • Kalman Filter │ • XGBoost Risk Classifier   │ • 5 Languages (EN/HI/BN/    │
│ • Edge Contract │ • Isolation Forest Anomaly  │   TA/SAT)                   │
└─────────────────┴─────────────────────────────┴─────────────────────────────┘
```

### Data & Inference Pipeline
```
[Sensors: Tilt / Crack / Gas / Vib]
                │ (LoRa / MQTT)
                ▼
      [Mosquitto Broker]
                │
      [Edge Ingest Loop] ──► [Kalman Signal Filter]
                │
                ├──► [TimescaleDB / PostGIS Storage]
                ├──► [Redis Telemetry Cache]
                │
      [ML Inference Service]
         ├── XGBoost Classifier (18 Features: Tilt, Vib RMS, Crack, Strain...)
         └── Isolation Forest (Anomaly Score vs 0.6500 Threshold)
                │
                ▼ (WebSocket Broadcast / SSE)
    ┌───────────────────────────┬───────────────────────────┐
    ▼                           ▼                           ▼
[3D Digital Twin Scene]   [GIS Geospatial Map]    [Mobile Worker Client]
(Crown pillar deformation) (Dynamic A* evacuation) (Push siren, Provenance)
```

---

## 🚀 Key Features (Implemented)

### 1. Dual AI Anomaly & Risk Engine
- **XGBoost 18-Feature Risk Engine (`xgb_risk_v3`)**: Predicts geotechnical risk categories (`NORMAL`, `ELEVATED`, `WARNING`, `CRITICAL`, `HAZARD`) based on displacement, tilt magnitude, crack expansion, vibration energy bands, extraction ratio, and geological depth.
- **Isolation Forest Multivariate Detector**: Continuously audits incoming sensor streams against calibrated baseline distributions to flag strata movement anomalies before visual cracking occurs.
- **Kalman Filtering**: Suppresses transient machine noise and blasting vibrations from underlying structural movement.

### 2. Web Command Center & 3D Digital Twin
- **Interactive 3D WebGL Scene (`Mine3DScene.jsx`)**: Built with Three.js and `@react-three/fiber`, visualizing mine shafts, extraction panels, crown pillars, stress-strain deformation cones, and sensor beacon statuses.
- **GIS Risk Mapping (`Mine2DMap.jsx`, `RiskMap.jsx`)**: Open-source Leaflet map displaying pit zones, worker locations, beacon telemetry, and computed dynamic evacuation paths.
- **Auditory Alert System**: Synthesized industrial siren alerts with HTML5 fallback for Caution, Warning, and Critical events (`critical.mpeg`, `warning.mpeg`, `critical.mp3`, `warning.mp3`).
- **Reporting Engine**: Generates automated shift compliance reports and technical safety summaries (`pdf_generator.py`).

### 3. Cross-Platform Mobile Application (`mobile/`)
- **React Native & Expo SDK 57**: Production-ready field client for miners and shift supervisors.
- **Real-Time WebSocket Synchronization**: Instant hazard broadcasts, zone state updates, and biometric telemetry.
- **Data Provenance System**: `ProvenanceBadge` component verifying pipeline integrity and cryptographic validation for every received alert.
- **5-Language Localization**: English (`en`), Hindi (`hi`), Bengali (`bn`), Tamil (`ta`), and Santali (`sat`).

### 4. Edge Hardware Contract
- **Contract Verification (`validate_edge_contract.py`)**: 35-check test harness verifying checksums, range boundaries, simulator schema compliance, and fail-safe operational modes.

---

## 🛠️ Technology Stack

| Layer | Technologies |
| :--- | :--- |
| **Backend** | Python 3.12+, FastAPI, SQLAlchemy 2.0, Pydantic v2, Alembic, Uvicorn, Structlog |
| **AI / ML** | XGBoost, Scikit-learn (Isolation Forest), Pandas, NumPy, SciPy, Joblib |
| **Databases** | PostgreSQL 16, TimescaleDB (Hypertables), PostGIS (EPSG:4326), Redis 7 |
| **Broker** | Eclipse Mosquitto (MQTT) |
| **Web Dashboard** | React 19, Vite 8, Tailwind CSS, Three.js, React Three Fiber, Leaflet, Recharts, i18next, Lucide React |
| **Mobile App** | React Native 0.86, Expo SDK 57, TypeScript 6.0, React Navigation, AsyncStorage, Jest |
| **Testing** | Pytest, Vitest, Jest, Jest-Expo, Oxlint |

---

## 📂 Repository Structure

```
TerraMesh-AI/
├── apps/
│   └── mineguard-core/
│       ├── backend/                 # FastAPI service & AI inference engine
│       │   ├── main.py              # Application entry point & API routes
│       │   ├── database.py          # PostgreSQL / TimescaleDB engine
│       │   ├── spatial.py           # PostGIS geospatial processing
│       │   ├── ml_service.py        # XGBoost & Isolation Forest inference
│       │   ├── edge_ingest_loop.py  # MQTT edge message processing
│       │   ├── ml/                  # ML training scripts & evaluations
│       │   ├── models/              # Pretrained joblib models & metadata
│       │   ├── reports/             # PDF report generator
│       │   └── tests/               # Backend test suites
│       ├── edge/                    # Edge schemas & hardware contracts
│       │   └── contracts/           # edge_model_contract.json
│       └── frontend/                # React 19 Web Command Center
│           ├── src/
│           │   ├── components/      # 3D Scene, GIS Map, KPI panels, Modals
│           │   ├── context/         # MineDataContext, AuthContext
│           │   ├── i18n/            # Translations (en, hi, bn, ta, sat)
│           │   └── services/        # API client, initialConfig
│           └── public/              # Static assets, audio alerts & icons
├── mobile/                          # Expo / React Native mobile app
│   ├── src/
│   │   ├── components/              # ProvenanceBadge, Header, UI widgets
│   │   ├── features/                # Evacuation, Monitoring, Settings screens
│   │   ├── i18n/                    # Mobile translations (en, hi, bn, ta, sat)
│   │   └── services/                # Mobile API & WebSocket client
│   └── __tests__/                   # Jest test suites (API, i18n, components)
├── docs/                            # Comprehensive engineering & SOP documentation
├── infra/                           # Docker, Nginx, and Mosquitto configuration
├── docker-compose.yml               # Multi-container orchestration
├── LICENSE                          # MIT License
└── README.md                        # Documentation
```

---

## ⚙️ Getting Started

### Prerequisites
- **Docker & Docker Compose** (for full infrastructure stack)
- **Node.js 18+** & **Bun** or **npm**
- **Python 3.11+**

### 1. Clone Repository
```bash
git clone https://github.com/calyxion/TerraMesh-AI.git
cd TerraMesh-AI
```

### 2. Infrastructure Setup (Docker Compose)
Start PostgreSQL, TimescaleDB, Redis, and Mosquitto:
```bash
docker compose up -d postgres redis mosquitto
```

### 3. Backend Setup
```bash
cd apps/mineguard-core/backend
python -m venv venv
# Windows:
.\venv\Scripts\activate
# Linux/macOS:
source venv/bin/activate

pip install -r requirements.txt
cp .env.example .env

# Run FastAPI backend
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```
API documentation is automatically served at: `http://localhost:8000/docs`

### 4. Frontend Web Dashboard Setup
```bash
cd apps/mineguard-core/frontend
npm install
npm run dev
```
Open `http://localhost:5173` in your browser.  
Default demo credentials:
- **Email**: `admin@terramesh.gov.in`
- **Password**: `admin`

### 5. Mobile Application Setup
```bash
cd mobile
npm install
npm start
```
Scan the QR code with the Expo Go app on Android/iOS, or press `a` for Android Emulator.

---

## 🧪 Testing & Verification

Each tier of TerraMesh AI has automated validation:

### Edge Model Contract Validation
```bash
python apps/mineguard-core/backend/validate_edge_contract.py
# Result: 35 passed, 0 failed — CONTRACT VALID
```

### Backend ML Pipeline Unit Tests
```bash
pytest apps/mineguard-core/backend/test_ml_integration.py -v
# Result: 1 passed in ~2.2s
```

### Frontend Web Unit Tests & Build
```bash
cd apps/mineguard-core/frontend
npm test        # Vitest: 18 passed in 1 test suite
npm run build   # Production bundle built in ~1.6s
```

### Mobile TypeScript Check & Jest Test Suite
```bash
cd mobile
npm run typecheck   # Clean TypeScript verification
npm test            # Jest: 4 test suites passed (33 tests)
```

---

## 📦 Releases & Artifacts

Pre-built production bundles are available under [GitHub Releases](https://github.com/calyxion/TerraMesh-AI/releases):
- `terramesh-web-dashboard-v1.0.0.zip`: Production HTML5/CSS3/JavaScript assets for the Web Command Center.
- `terramesh-mobile-android-v1.0.0.zip`: Exported Hermes bytecode and asset bundle for Android.
- `checksums.txt`: SHA-256 integrity checksums for all release binaries.

---

## ⚠️ Limitations & Scope
- **Field Hardware**: Physical LoRa mesh hardware is simulated via the hardware-in-the-loop edge contract (`validate_edge_contract.py`); live subterranean deployment is subject to field mine trials.
- **Safety Regulations**: Thresholds and classifications are aligned with DGMS circulars and the Coal Mines Regulations (CMR) 2017 standards for Indian coalfields.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE) — see the `LICENSE` file for details.
