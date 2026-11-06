# TerraMesh-AI v1.0.0 Release Notes

**TerraMesh-AI (MineGuard AI)** — AI-Powered Mine Subsidence Monitoring & Underground Coal Mine Safety Command Center (SIH26025).

---

## Highlights

### 1. Multi-Model AI Risk & Anomaly Engine
- **XGBoost Risk Classifier (`xgb_risk_v3`)**: 18-feature inference engine evaluating geotechnical tilt, displacement velocity, crack expansion, acoustic emissions, and extraction ratios.
- **Isolation Forest Anomaly Detection**: Multivariate detection of subtle strata deformation and sensor anomalies.
- **Kalman Filtering**: Eliminates high-frequency blast/machinery vibration noise from structural movement.
- **Subsidence Trend Forecaster**: Predicts crown pillar displacement velocity and time-to-failure.

### 2. Interactive 3D Digital Mine Twin & Web Command Center
- **Three.js WebGL Scene (`Mine3DScene.jsx`)**: Real-time rendering of underground galleries, crown pillars, subsidence strain cones, fault lines, and live sensor telemetry beacons with full orbit controls.
- **GIS Geospatial Risk Map**: Leaflet GIS map with mining zone risk color-coding, worker tracking, biometric status, and dynamic A* evacuation corridor routing.
- **Auditory Alert Broadcasts**: Multi-frequency siren synthesizer with HTML5 fallback for caution, warning, and critical alert events.

### 3. Multilingual Mobile Field Application
- **Cross-Platform Expo / React Native (`mobile/`)**: Worker companion application with real-time WebSocket live streaming.
- **5 Supported Languages**: English, Hindi (`hi`), Bengali (`bn`), Tamil (`ta`), and Santali (`sat`).
- **Data Provenance**: End-to-end cryptographic and pipeline audit verification via `ProvenanceBadge`.

### 4. Edge Hardware-in-the-Loop Contract
- Formal 35-point edge hardware contract (`edge_model_contract.json`) validated across firmware schema, range boundaries, and model checksums.
- Packet deduplication, timestamp sanity filtering, and fail-safe degraded mode fallbacks.

---

## Release Artifacts & Checksums

| Artifact | Description | SHA-256 Checksum |
| :--- | :--- | :--- |
| `terramesh-web-dashboard-v1.0.0.zip` | Production build of the Web Command Center (HTML/JS/CSS assets) | `D5C648EB1DF11694363685C36EF4F8A7A37ADF7F384EDA1F8C2C787497D75EC5` |
| `terramesh-mobile-android-v1.0.0.zip`| Exported production Hermes bytecode bundle and assets for Android | `F98081CDE187FB84CBCF89093D929F3DC0699B7C90CB926DD5EE6E5DD61F3518` |

---

## Installation & Deployment

### Web Dashboard
Extract `terramesh-web-dashboard-v1.0.0.zip` into any static web server (Nginx, Apache, or Firebase Hosting):
```bash
unzip terramesh-web-dashboard-v1.0.0.zip -d /var/www/html/
```

### Full Backend & Infrastructure
Deploy via Docker Compose:
```bash
git clone https://github.com/calyxion/TerraMesh-AI.git
cd TerraMesh-AI
cp apps/mineguard-core/backend/.env.example apps/mineguard-core/backend/.env
docker compose up -d
```

### Mobile Application (Android APK Build)
Build an installable APK using EAS Build or a Linux Android NDK container:
```bash
cd mobile
npx eas-cli build --platform android --profile preview
```

---

## Verification Summary
- **Edge Model Contract**: 35 checks passed (0 failed).
- **Backend Unit Tests**: 28 passed.
- **Frontend Vitest**: 18 passed.
- **Mobile Jest**: 4 test suites passed (33 tests).
- **Mobile TypeScript**: Clean typecheck (`tsc --noEmit`).
- **Secret Scan**: 0 embedded secrets detected.
- **i18n Parity**: Full parity across all 5 languages.

