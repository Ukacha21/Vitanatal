# 🌿 Project No-Sezaryen (VITA-NATAL)
## IoT-Enabled Maternal-Fetal Health Monitoring & Fetal Presentation Tracking System
### Engineering Safe, Natural Vaginal Births & Minimizing Avoidable Cesarean Surgeries

---

## 📌 Executive Summary

**Project No-Sezaryen (Codename: VITA-NATAL / Doğal Doğum Teknolojisi)** is an intelligent biomedical mechatronics and IoT ecosystem designed to **prevent avoidable cesarean sections (C-sections)** and empower women toward safe, confident, natural vaginal deliveries.

The system combines:
1. **A Wearable Multi-Modal Abdominal Tracker ("PartusBand"):** An ultra-comfortable, medical-grade ergonomic wearable band equipped with an array of **Passive Acoustic Auscultation (fPCG) MEMS microphones**, **Uterine Electromyography / Fetal ECG (EHG/fECG) electrodes**, and **Multi-Quadrant 6-DoF Inertial Measurement Units (IMUs)**.
2. **An On-Device TinyML Presentation Engine:** A real-time edge algorithm that correlates fetal cardiac valve acoustics with localized limb impulse kick centroids to **continuously determine and predict fetal presentation** (Cephalic/Vertex vs. Breech vs. Transverse vs. Posterior) from the second trimester through active labor.
3. **True Labor Predictive Analytics:** Non-invasive monitoring of uterine contraction electrophysiology (EHG burst frequency and power spectra) to differentiate between **Braxton Hicks (false labor)** and **Active Labor Progression**, preventing premature hospital admission—one of the leading clinical catalysts of failed induction and emergency C-sections.
4. **An Interactive Companion Mobile Application ("MaternaSafe"):** Delivering continuous fetal wellbeing reassurance (FHR baseline, variability, kick counts), guided biomechanical maternal postural routines (Spinning Babies / pelvic rocking) to turn breech fetuses early, and automated Non-Stress Test (NST/CTG) telemetry exports for obstetricians.

---

## 📂 Project Files & Presentation Deck Index

| Document | Format | Description |
| :--- | :--- | :--- |
| 📽️ **[presentation.html](./presentation.html)** | **Interactive Web Slide Deck** | 14-slide standalone keynote with keyboard navigation, progress bar, fullscreen toggle, and speaker notes drawer. |
| 📑 **[presentation.md](./presentation.md)** | **Presentation Script & Defense Deck** | Complete slide-by-slide script, spoken presenter talking points, visual layout notes, and OB-GYN Q&A defense. |
| ⚡ **[hardware_specifications.md](./hardware_specifications.md)** | **IoT Hardware & Schematics Blueprint** | Component selection (TI ADS1298, Knowles MEMS, Bosch BMA456, Nordic nRF5340), power budget, and IP67 enclosure. |
| 🧠 **[fetal_position_algorithm.md](./fetal_position_algorithm.md)** | **TinyML Algorithm & Derivation** | Mathematical formulation of Spatial Heart-Kick Vectoring (SHKV) and Uterine EHG burst labor triage. |
| 📱 **[mobile_app_spec.md](./mobile_app_spec.md)** | **Companion Mobile Application Spec** | Flutter architecture, custom BLE 5.3 GATT service (`0xFD50`), and 5 core maternal & clinical screens. |
| 📚 **[clinical_rationale_and_guidelines.md](./clinical_rationale_and_guidelines.md)** | **Clinical Evidence & References** | WHO statistics, gestational breech version timeline, FIGO/ACOG guidelines, and peer-reviewed bibliography. |

---

## 🎯 Clinical Problem Statement & Motivation

### The Global Cesarean Section Crisis
- The **World Health Organization (WHO)** states that national cesarean rates above **10% to 15%** offer no maternal or neonatal benefit and introduce unnecessary surgical risks (infection, hemorrhage, neonatal respiratory distress, uterine rupture in subsequent pregnancies).
- In reality, cesarean rates in countries like **Türkiye (>58%)**, **Brazil (>55%)**, and across private clinics globally exceed **60–70%**.

### Why Do Avoidable Cesarean Deliveries Occur?

| Clinical Factor | Traditional Clinical Dilemma | How Project No-Sezaryen Solves It |
| :--- | :--- | :--- |
| **Late Breech Detection** | Breech (head-up) position is often confirmed late (Week 37–39), leaving no time for non-invasive rotation. A planned C-section is automatically booked. | **Continuous Vector Presentation Tracking:** Detects persistent breech presentation between Weeks 28–34; guides targeted maternal pelvic posturing (70–85% natural cephalic version rate) and alerts OB-GYN early for External Cephalic Version (ECV). |
| **Premature Admission & Failed Induction** | Mothers rush to the clinic during latent/false labor (Braxton Hicks). Clinicians administer synthetic oxytocin (Pitocin) to speed things up; if the cervix isn't ready, labor stalls and triggers an **Emergency C-Section**. | **Uterine EHG Burst Spectral Analysis:** Quantifies true uterine muscle synchronization vs. benign irritability, giving clear guidance on the optimal moment to enter the maternity ward. |
| **Occiput Posterior ("Sunny-Side Up") Labor** | Fetus faces the mother’s abdomen instead of the spine, causing severe prolonged back labor, cervical dystocia, and maternal exhaustion that cascades into surgical extraction. | **Real-Time Fetal Spine & Limb Orientation:** Identifies posterior rotation early in labor, guiding maternal side-lying and forward-leaning postures to rotate the occiput anteriorly. |
| **Fetal Distress Anxiety & Lack of Home Telemetry** | Mothers feel anxious between infrequent clinic visits, opting for elective surgical delivery out of fear of stillbirth or cord accidents. | **24/7 Passive Non-Invasive Reassurance:** Daily fetal heart rate (FHR) tracking, baseline variability checks, and automated kick actigraphy without high-energy continuous ultrasound. |

---

## 🔬 System Architecture Overview

```
                 ┌──────────────────────────────────────────────────────────┐
                 │          WEARABLE MATERNAL-FETAL ABDOMINAL BAND          │
                 │                      ("PartusBand")                      │
                 └────────────────────────────┬─────────────────────────────┘
                                              │
         ┌────────────────────────────────────┼────────────────────────────────────┐
         │                                    │                                    │
         ▼                                    ▼                                    ▼
┌──────────────────┐               ┌──────────────────┐               ┌──────────────────┐
│  fECG / EHG AFE  │               │ fPCG Acoustic    │               │ 4-Quadrant IMU   │
│  Electrode Array │               │ Contact Sensors  │               │ Impulse Matrix   │
│ (ADS1298 / AgCl) │               │ (MEMS Mics Array)│               │ (Bosch BMA456)   │
└────────┬─────────┘               └────────┬─────────┘               └────────┬─────────┘
         │                                  │                                  │
         │ (Uterine Bursts & FHR)           │ (Acoustic Heart Focus)           │ (Limb Kicks)
         └──────────────────────────────────┼──────────────────────────────────┘
                                            │
                                            ▼
                 ┌──────────────────────────────────────────────────────────┐
                 │               ULTRA-LOW POWER EMBEDDED MCU               │
                 │              (Nordic nRF5340 / ESP32-S3)                 │
                 │                                                          │
                 │  • Dual-Core ARM Cortex-M33 Processing                   │
                 │  • Signal Pre-Filtering & Denoising (Wavelet / Notch)     │
                 │  • On-Device TinyML Fetal Vector Presentation Engine     │
                 │  • BLE 5.3 Long-Range Encrypted Telemetry                │
                 └──────────────────────────┬───────────────────────────────┘
                                            │
                                  BLE 5.3 Encrypted Sync
                                            │
                                            ▼
                 ┌──────────────────────────────────────────────────────────┐
                 │               COMPANION MOBILE APPLICATION               │
                 │                      ("MaternaSafe")                     │
                 │                                                          │
                 │  • Real-Time Fetal Presentation Compass (Head-Down/Breech)│
                 │  • Fetal Heart Rate Reassurance & Daily Kick Actigram    │
                 │  • Labor Progression Engine (Braxton Hicks vs. True Labor)│
                 │  • Guided Biomechanical Pelvic Alignment Routines        │
                 │  • Clinician Remote Telemetry Non-Stress Test (NST) Portal│
                 └──────────────────────────────────────────────────────────┘
```

---

## 🛠️ Hardware & Sensor Subsystems

### 1. Electrophysiological Array: Fetal ECG & Electrohysterogram (fECG / EHG)
- **Clinical Role:** Captures the electrical activity of the uterine myometrium (contractions) and the micro-volt electrical signals of the fetal heart.
- **Components:**
  - **Texas Instruments ADS1298 / Analog Devices AD8426:** 24-bit multi-channel low-noise biosensing Analog Front End (AFE) with integrated Right Leg Drive (RLD) for common-mode rejection (>115 dB CMRR).
  - **Differential Filtering Pipeline:**
    - **fECG Bandpass (10 Hz – 100 Hz):** Extracts fetal QRS complexes (~5–20 µV) masked by maternal QRS complexes (~1 mV) using Blind Source Separation (FastICA).
    - **EHG Bandpass (0.1 Hz – 3.0 Hz):** Captures slow electrical slow waves and rapid action potential bursts of uterine muscle contractions.

### 2. Passive Phono-Auscultation Sensor Array (fPCG)
- **Clinical Role:** Detects mechanical acoustic heart sounds ($S_1, S_2$ valve closures) completely passively—eliminating the continuous acoustic energy output of Doppler ultrasound transducers.
- **Components:**
  - 4× Precision acoustic contact piezoelectric / MEMS acoustic transducers placed in the 4 quadrants of the abdomen:
    - Quadrant 1: Right Upper Quadrant (RUQ)
    - Quadrant 2: Left Upper Quadrant (LUQ)
    - Quadrant 3: Right Lower Quadrant (RLQ)
    - Quadrant 4: Left Lower Quadrant (LLQ)
  - Acoustic signal conditioning: Low-noise active bandpass (20 Hz – 180 Hz) with dynamic thresholding to isolate cardiac acoustic peaks.

### 3. Four-Quadrant Inertial Kick-Tracking Matrix (IMU Actigraphy)
- **Clinical Role:** Tracks localized mechanical surface accelerations caused by fetal kicks, punches, and somersaults.
- **Components:**
  - 4× **Bosch BMA456** ultra-low power 16-bit triaxial accelerometers with integrated hardware tap/step engines.
  - Placed at the spatial extremities of the band across maternal abdominal quadrants.
  - Differentiates maternal respiratory/walking motions (low frequency <2 Hz, broad spatial distribution) from acute fetal limb impacts (sharp transient spikes >5 Hz localized to a single quadrant).

### 4. Embedded Compute & Power Subsystem
- **Main Controller:** **Nordic Semiconductor nRF5340** (Dual-core ARM Cortex-M33; 128 MHz Application Core + 64 MHz Network Core) or **Espressif ESP32-S3** with Vector Extensions.
- **Power Management:**
  - Ultra-thin 850 mAh Medical Li-Polymer battery with overcharge/short-circuit protection.
  - Qi-standard inductive wireless charging (sealed waterproof IP67 enclosure, easy cleaning and disinfection).
  - 24+ hour continuous monitoring per charge.

---

## 🧠 Fetal Position & Presentation Prediction Algorithm

### Spatial Heart-Kick Vectoring (SHKV)
Traditional medical checks use ultrasound or manual Leopold’s Maneuvers to determine fetal presentation. Project No-Sezaryen automates this through **Spatial Heart-Kick Vectoring**:

1. **Acoustic Heart Centroid ($\vec{C}_{\text{heart}}$):**
   $$\vec{C}_{\text{heart}} = \frac{\sum_{i=1}^{4} w_i \cdot \vec{P}_{\text{mic}, i}}{\sum_{i=1}^{4} w_i}$$
   where $w_i$ is the acoustic SNR of heart valve closures detected at microphone position $\vec{P}_{\text{mic}, i}$.
   - If $\vec{C}_{\text{heart}}$ lies in the lower quadrants (pelvic baseline) $\rightarrow$ The fetal thorax is oriented downward.
   - If $\vec{C}_{\text{heart}}$ lies in the upper quadrants (fundal baseline) $\rightarrow$ The fetal thorax is oriented upward.

2. **Kinetic Kick Centroid ($\vec{C}_{\text{kick}}$):**
   $$\vec{C}_{\text{kick}} = \frac{1}{N} \sum_{k=1}^{N} \vec{P}_{\text{IMU}, k}$$
   derived from the spatial center of impulse kicks recorded over a rolling 4-hour window. Since the strongest kicks originate from the lower limbs (feet and knees):
   - Upper fundal kicks + Lower pelvic heart sounds = **Cephalic / Vertex Presentation (Head-Down) 🟢**
   - Lower pelvic kicks + Upper fundal heart sounds = **Breech Presentation (Head-Up) 🔴**
   - Lateral left/right kicks + Central heart sound = **Transverse Lie (Shoulder Presentation) 🟡**

3. **Presentation Trajectory & Early Warning Engine:**
   - **Week 20–28:** Fetus rotates freely. System records baseline mobility actigrams.
   - **Week 28–32:** Stabilization window. System tracks rotation frequency.
   - **Week 32–35:** If breech presentation persists continuously for >7 days, the system triggers the **Biomechanical Version Coaching Protocol** via the mobile app.
   - **Week 36+:** Clinical alert for hospital consultation and potential **External Cephalic Version (ECV)** before amniotic fluid volume decreases.

---

## ⚡ True Labor vs. Braxton Hicks Classifier

To prevent early maternal admission and cascade-to-cesarean interventions:

```
Uterine Contraction Signal (EHG)
              │
              ▼
   Wavelet Decomposition (db4)
              │
              ▼
┌──────────────────────────────────────────────┐
│  Peak Frequency ($F_{\text{peak}}$):         │
│  • Braxton Hicks: 0.10 Hz – 0.25 Hz          │
│  • True Active Labor: 0.35 Hz – 0.85 Hz      │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│  Uterine Propagation Velocity:               │
│  • Braxton Hicks: Disorganized, localized    │
│  • True Active Labor: Coordinated (2–5 cm/s) │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│  CLASSIFICATION RESULT:                      │
│  🟢 Latent / Benign: Rest & hydrate at home  │
│  🚨 True Labor Onset: Prepare for hospital   │
└──────────────────────────────────────────────┘
```

---

## 📱 Mobile Application Architecture ("MaternaSafe")

### Core Screens & Features

1. **Fetal Compass & Presentation Dial:**
   - Graphical 3D visualization showing the baby’s orientation inside the pelvis.
   - Status indicators: `Head-Down (Cephalic - Vertex)` (Safe for natural birth), `Breech`, `Transverse`, `Occiput Posterior`.
2. **Fetal Wellbeing & Non-Stress Test (NST):**
   - Fetal Heart Rate monitor (110–160 bpm nominal range).
   - Baseline variability scoring and acceleration tracking.
   - Interactive 24-hour kick count actigram.
3. **Natural Birth Coaching & Breech Turning Guide:**
   - Step-by-step interactive video routines tailored to current fetal position:
     - **Forward-Leaning Inversion (FLI):** Relaxes uterine ligaments to give breech babies room to flip.
     - **Pelvic Tilts & Cat-Cow Stretches:** Loosens pelvic floor muscles.
     - **Side-Lying Release (SLR):** Addresses maternal pelvic torsions.
     - **Birthing Ball Figure-8s:** Encourages optimal engagement of the baby's head.
4. **Labor Contraction Timer & Hospital Go-Time Gauge:**
   - Automated 5-1-1 rule tracker (Contractions 5 minutes apart, lasting 1 minute, for 1 hour).
   - EHG-backed true labor validation index to avoid premature clinic admission.
5. **OB-GYN Telemetry Export:**
   - One-touch PDF / DICOM export of 20-minute cardiotocography non-stress test reports.

---

## 📋 Comprehensive Project Roadmap

### Phase 1: Biomedical Transducer Prototyping (Months 1–3)
- [ ] Assemble 4-quadrant analog front-end with ADS1298 and MEMS acoustic microphones.
- [ ] Fabricate flexible prototype belt using skin-safe medical silicone.
- [ ] Validate fECG extraction algorithms against public PhysioNet Non-Invasive Fetal ECG datasets.

### Phase 2: Firmware & TinyML Position Model (Months 4–6)
- [ ] Implement FastICA and wavelet denoising on Nordic nRF5340 ARM Cortex-M33.
- [ ] Train Spatial Heart-Kick Vectoring (SHKV) classifier using synthetic biomechanical motion models.
- [ ] Achieve BLE 5.3 telemetry streaming with <15 mA active power consumption.

### Phase 3: Mobile App & User Experience (Months 7–9)
- [ ] Develop cross-platform mobile application (Flutter / React Native).
- [ ] Implement offline-first local SQLite sync and Bluetooth GATT profile.
- [ ] Build guided maternal posturing module with interactive timers.

### Phase 4: Clinical Benchmarking & Ethical Validation (Months 10–12)
- [ ] Benchmark position estimates against clinical 2D/3D obstetric ultrasound scans.
- [ ] Validate EHG contraction detection against traditional tocodynamometry (TOCO).
- [ ] Prepare CE MDR (Class IIa) / FDA 510(k) regulatory documentation.

---

## 🛡️ Biocompatibility & Clinical Safety
- **100% Passive Sensing:** Zero continuous ultrasound radiation, zero thermal heating, zero mechanical vibration.
- **Biocompatible Materials:** ISO 10993 compliant medical silicone and silver-chloride dry electrodes.
- **Data Security & Privacy:** End-to-end AES-128 BLE encryption with HIPAA / GDPR compliant cloud storage.

---

## 👥 Project Team & Contributors
- 👩‍💻 **Karimah Zubair** — Computer Engineering · Co-Developer & Project Teammate · [LinkedIn Profile](https://www.linkedin.com/in/karima-zoubir-78109b3b5)
- 👨‍💻 **Ukacha Atumane Juma** — Mechatronics Engineering & Embedded Systems Lead · [GitHub Profile](https://github.com/Ukacha21) · [LinkedIn Profile](https://linkedin.com/in/ukacha)

---

*Project Repository: [https://github.com/Ukacha21/Vitanatal](https://github.com/Ukacha21/Vitanatal)*  
*Portfolio Showcase: [https://ukacha.com/project/vitanatal](https://ukacha.com/project/vitanatal)*  
*Selçuk University Mechatronics Engineering*
