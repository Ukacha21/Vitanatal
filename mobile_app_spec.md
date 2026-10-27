# 📱 Mobile Application & Telemetry Specifications
## "MaternaSafe" Companion App for Natural Birth Empowerment

---

## 1. Application Architecture & Tech Stack

- **Framework:** **Flutter** (Dart) or **React Native** (TypeScript) for cross-platform iOS & Android performance.
- **Local Database:** **SQLite** with **SQLCipher** for offline-first encrypted storage of medical telemetry.
- **Hardware Communication:** **CoreBluetooth (iOS) / Android BLE API** via custom Bluetooth Low Energy (BLE 5.3) GATT profile.
- **Backend Infrastructure:** **Go / FastAPI** microservice hosted on HIPAA/GDPR-compliant infrastructure with WebSockets for real-time clinician monitoring.

```
+---------------------------------------------------------------------------------------+
|                               "MATERNASAFE" MOBILE CLIENT                             |
|                                                                                       |
|   +-----------------------+     +-----------------------+     +-------------------+   |
|   |      BLE ENGINE       |     |  LOCAL SQLCIPHER DB   |     |    REACTIVE UI    |   |
|   |  GATT Auto-Reconnect  |---->| Encrypted Time-Series |---->| Fetal Compass 3D  |   |
|   |  AES-128 Decryption   |     | Telemetry Storage     |     | Contraction Timer |   |
|   +-----------------------+     +-----------------------+     | Coaching Modules  |   |
|                                             |                 +-------------------+   |
|                                             v                           |             |
|                                 +-----------------------+               |             |
|                                 |   SYNC & REPORTING    |               |             |
|                                 | Cloud Telemetry Sync  |<--------------+             |
|                                 | PDF Non-Stress Export |                             |
|                                 +-----------------------+                             |
+---------------------------------------------+-----------------------------------------+
                                              | HTTPS / WSS Encrypted
                                              v
+---------------------------------------------------------------------------------------+
|                              OB-GYN / CLINICIAN WEB PORTAL                            |
|                                                                                       |
|  • Real-Time Non-Stress Test (NST) Cardiotocogram Traces                              |
|  • Longitudinal Fetal Presentation Trajectory (Weeks 20 - 40)                         |
|  • Uterine EHG Contraction Electrophysiology & Labor Onset Alerts                     |
|  • Automatic Flagging for Persistent Breech at Week 35 (ECV Candidate Alert)          |
+---------------------------------------------------------------------------------------+
```

---

## 2. Bluetooth Low Energy (BLE) GATT Architecture

### Primary Custom Service: `VITA_NATAL_SERVICE` (`UUID: 0xFD50`)

| Characteristic Name | UUID | Properties | Description |
| :--- | :--- | :--- | :--- |
| **`FETAL_HEART_RATE`** | `0x2D31` | `Read`, `Notify` | Fetal heart rate in BPM (uint8), baseline variability (uint8), signal quality index (uint8). |
| **`FETAL_PRESENTATION`** | `0x2D32` | `Read`, `Notify` | Presentation class: `0x00=Cephalic`, `0x01=Breech`, `0x02=Transverse`, `0x03=Occiput Posterior`, confidence score (0–100%). |
| **`KICK_IMPULSE_STREAM`**| `0x2D33` | `Notify` | Timestamp, quadrant ID (1–4), kick intensity magnitude ($g$-force $\times 100$). |
| **`UTERINE_CONTRACTION`**| `0x2D34` | `Notify` | Contraction status (`Active / Latent`), EHG RMS power, peak frequency ($F_{\text{peak}} \times 100 \text{ Hz}$). |
| **`BATTERY_DEVICE_STATUS`**| `0x2A19`| `Read`, `Notify` | Standard battery percentage (0–100%), charging status, lead impedance checks. |

---

## 3. Core Mobile UI Screens & Functional Breakdown

### Screen 1: The Fetal Compass (Home Dashboard)
- **Visual Centerpiece:** An interactive 3D rendering of the pregnant abdomen showing the baby's current orientation:
  - **Head Down (Cephalic / Vertex) 🟢:** Celebratory reassuring banner ("Baby is in the ideal position for a natural vaginal delivery").
  - **Head Up (Breech) 🔴:** Supportive, proactive banner ("Baby is currently breech. Let's practice your 15-minute gentle pelvic alignment routine").
  - **Transverse Lie 🟡:** Guidance banner ("Baby is lying sideways. Follow our side-lying release exercises").
- **Vital Quick Stats:**
  - Current FHR: `138 BPM` (Normal 110–160 BPM).
  - Daily Kicks: `34 kicks` (Normal active score).
  - Last Position Check: `Updated 12 mins ago`.

### Screen 2: 24-Hour Fetal Kick & Wellbeing Tracker
- **Fetal Actigram:** Graphical bar chart tracking kick frequency across morning, afternoon, and evening.
- **Sleep/Wake Cycles:** Automatically tags fetal active vs. resting periods to prevent unnecessary maternal anxiety during normal fetal sleep cycles (typically 20–40 minutes).
- **Abnormal Movement Alert:** Flags sustained hypomobility ($<10$ kicks in 2 hours during expected active windows) for clinical follow-up.

### Screen 3: Natural Birth & Breech-Turning Coaching
- **Targeted Postural Library:**
  - **Forward-Leaning Inversions (FLI):** Guided 30-second timer with safety checkpoints (pillows, assistant presence).
  - **Pelvic Tilts & Cat-Cow:** Audio-guided rhythm for optimal pelvic mobility.
  - **Birthing Ball Circular Exercises:** Pelvic opening guidance for Weeks 36–40.
- **Progress Tracking:** Tracks adherence to positional exercises and documents the exact date/hour the baby successfully flips to cephalic!

### Screen 4: Contraction Timer & Labor Go-Time Engine
- **Automated Contraction Detection:** Works automatically using the band’s EHG sensors—no manual button pressing required!
- **True Labor vs. Braxton Hicks Gauge:**
  - Real-time spectral indicator showing whether uterine contractions are disorganized Braxton Hicks or progressive active labor.
- **The "Go to Hospital" Alert:** Triggered when the clinical 5-1-1 rule is fulfilled with validated true labor EHG spectral power:
  - *Contractions 5 minutes apart, lasting 60 seconds, consistent for 1 full hour.*
  - Directly reduces premature hospital admission and avoidable emergency surgical interventions.

### Screen 5: Clinician Export & Non-Stress Test (NST) Report
- **One-Touch PDF Generation:** Generates an official Non-Stress Test (NST) Cardiotocogram trace compliant with FIGO / ACOG guidelines:
  - Upper channel: Continuous Fetal Heart Rate trace (100–180 BPM).
  - Lower channel: Uterine Tocogram / EHG contraction bursts.
  - Baseline Heart Rate, Accelerations count ($\ge 15 \text{ BPM}$ for $\ge 15 \text{ s}$), and Decelerations analysis.
- **Secure Share:** Direct encrypted sharing via email, WhatsApp, or clinic EHR portal.
