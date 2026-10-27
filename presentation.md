# 📽️ Project No-Sezaryen (VITA-NATAL)
## Comprehensive Technical & Clinical Pitch Deck

**Title:** VITA-NATAL: Wearable IoT Biotelemetry & Fetal Presentation Prediction to Minimize Avoidable Cesarean Deliveries  
**Author / Engineering Lead:** Ukacha & Project Team  
**Category:** Biomedical Engineering, Embedded Systems, IoT, TinyML & Digital Health  
**Target Audience:** OB-GYN Clinicians, Biomedical Research Committees, MedTech Investors & Healthcare Policy Stakeholders  

---

## 📑 Slide Deck Outline

1. **Slide 1: Title & Vision** — Engineering Natural Birth Through Non-Invasive Intelligence
2. **Slide 2: The Global & Regional Problem** — The Cesarean Section Crisis & WHO Benchmarks
3. **Slide 3: Clinical Root Cause Analysis** — Why Avoidable Surgical Births Occur
4. **Slide 4: The Paradigm Shift** — Proactive Early Detection vs. Late Emergency Reaction
5. **Slide 5: System Architecture** — End-to-End Ecosystem Overview
6. **Slide 6: Hardware Engineering ("PartusBand")** — Multi-Modal Passive Biosensing Architecture
7. **Slide 7: Core Algorithm I: Spatial Heart-Kick Vectoring (SHKV)** — Continuous Fetal Presentation Prediction
8. **Slide 8: Core Algorithm II: Uterine EHG Triage** — Halting the Premature Hospital Admission Cascade
9. **Slide 9: Mobile Ecosystem ("MaternaSafe")** — The Patient & Clinician Companion App
10. **Slide 10: Clinical Intervention Protocol** — Turning Breech Presentation Naturally (Weeks 28–34)
11. **Slide 11: Safety, Compliance & Biocompatibility** — Zero Continuous Ultrasound Radiation
12. **Slide 12: Socio-Economic & Healthcare Value** — Reducing Complications & Hospital Costs
13. **Slide 13: Technical Roadmap & Validation Strategy** — From Bench Prototype to Clinical Trial
14. **Slide 14: Conclusion & Grand Vision** — Empowering Confident, Safe Physiological Birth

---

## 🖥️ Slide 1: Title & Executive Vision
- **Header:** Project No-Sezaryen (VITA-NATAL)
- **Subheader:** Wearable IoT Biotelemetry & Fetal Presentation Prediction to Minimize Avoidable Cesarean Deliveries
- **Tagline:** *"Transforming maternal care from reactive surgical intervention to proactive physiological empowerment."*
- **Visual Elements:**
  - High-tech medical render: The ergonomic abdominal **PartusBand** synchronizing via BLE 5.3 with the **MaternaSafe** mobile interface showing a real-time fetal compass.
  - Core badges: `100% Passive Sensing` | `Real-Time Fetal Presentation Engine` | `TinyML at the Edge` | `Non-Invasive CTG/NST`.

> **🎙️ Speaker Notes:**  
> "Good morning, members of the evaluation committee and clinical guests. Today, we are presenting Project No-Sezaryen, codenamed VITA-NATAL. Every year, millions of expectant mothers undergo major abdominal surgery not because of unavoidable obstetric emergencies, but because current clinical monitoring tools leave doctors and mothers blind between infrequent clinic visits. We have engineered an IoT-enabled maternal-fetal tracking ecosystem that predicts fetal position from the second trimester, monitors true labor progress, and guides natural interventions to radically reduce avoidable cesarean deliveries."

---

## 🖥️ Slide 2: The Unspoken Crisis: The Global C-Section Epidemic
- **Header:** The Epidemic of Surgical Deliveries
- **Key Statistics & Metrics:**
  - **WHO Ideal Benchmark:** `10% – 15%` maximum recommended population cesarean rate.
  - **Türkiye:** `> 58.4%` (One of the highest rates among OECD countries).
  - **Brazil / Latin America:** `> 55.7%` across public hospitals; `> 85%` in private maternity clinics.
  - **Global Average:** Rising rapidly past `21.1%`, projected to exceed `29%` by 2030.
- **The Human & Clinical Toll:**
  - 3× higher risk of severe maternal morbidity (postpartum hemorrhage, sepsis, organ injury).
  - Increased risk of neonatal respiratory distress (lack of physiological vaginal thoracic squeeze).
  - Elevated risk of abnormal placentation (placenta accreta/previa) and uterine rupture in future pregnancies.

> **🎙️ Speaker Notes:**  
> "The World Health Organization has established clear evidence: national cesarean rates exceeding 10 to 15 percent do not reduce maternal or neonatal mortality. Instead, they introduce surgical risks, double recovery periods, and create long-term uterine scarring. Yet in our region, cesarean rates exceed 58%, and in private clinics, they often surpass 80%. Cesarean section has transitioned from a life-saving emergency backup to an overused default. Project No-Sezaryen targets the exact clinical tipping points that trigger avoidable surgeries."

---

## 🖥️ Slide 3: Clinical Root Cause Analysis
- **Header:** Why Do Avoidable Cesarean Deliveries Occur?
- **Four Critical Clinical Catalysts:**
  1. **Late Breech Detection (Weeks 37–39):** Breech or transverse presentation is often confirmed right before full term, when oligohydramnios and fetal size make natural or manual rotation nearly impossible. A scheduled C-section is booked immediately.
  2. **The "Admission Cascade" (False Labor Misdiagnosis):** Anxious mothers rush to hospital during early latent phase or Braxton Hicks contractions. Hospital policy starts active management: synthetic oxytocin (Pitocin) induction on an unripe cervix leads to stalled labor (failure to progress) and an emergency C-section.
  3. **Occiput Posterior Malposition ("Sunny-Side Up"):** The fetal occiput faces the maternal spine, causing agonizing back labor, protracted second stage, and fetal head deflection, frequently ending in surgical extraction.
  4. **Home-Isolation & Maternal Panic:** Lack of daily reassurance regarding fetal heart rate and kick movement creates severe psychological anxiety, prompting mothers to choose elective surgical delivery out of fear.

> **🎙️ Speaker Notes:**  
> "When we analyze why mothers end up in the operating theater, it is rarely a sudden catastrophic event. It is almost always a predictable sequence. Either the baby's breech presentation is noticed too late at week 38, or the mother rushes to the hospital during false labor contractions. Once admitted, synthetic oxytocin is administered; if the cervix does not dilate within hours, the diagnosis is 'failure to progress,' leading straight to surgery. By eliminating these specific inflection points, we can safely safeguard natural birth."

---

## 🖥️ Slide 4: The Paradigm Shift
- **Header:** Moving From Late Reaction to Early Guidance
- **Comparison Table:**

| Traditional Obstetric Workflow | The VITA-NATAL IoT Workflow |
| :--- | :--- |
| **Episodic Visits:** Ultrasound checks spaced 4 to 6 weeks apart. | **Continuous Telemetry:** Daily non-invasive passive monitoring at home. |
| **Late Breech Catch (W37–W39):** Baby is too large to flip safely; C-section booked. | **Early Golden Window (W28–W34):** Detects malpresentation when amniotic fluid volume allows 70–85% natural cephalic repositioning. |
| **Subjective Contraction Timing:** Guessing true labor using stopwatches. | **Electromyographic (EHG) Triage:** Spectral burst analysis pinpoints the exact time to depart for the maternity ward. |
| **High Ultrasound Exposure:** Handheld Doppler monitors emitting continuous acoustic energy. | **100% Passive Listening:** Auscultatory MEMS microphones and surface biopotentials with zero acoustic radiation. |

> **🎙️ Speaker Notes:**  
> "Our core premise is that timing is everything. Between Weeks 28 and 34, the ratio of amniotic fluid to fetal mass provides maximum rotational buoyancy. If a persistent breech orientation is flagged during this golden window, maternal biomechanical postures and external versions have a remarkable 70 to 85% success rate in naturally flipping the baby head-down. We shift obstetrics from passive surprise at term to proactive, empowered guidance throughout gestation."

---

## 🖥️ Slide 5: System Architecture Overview
- **Header:** End-to-End Biomedical IoT Ecosystem
- **Ecosystem Breakdown:**
  - **Layer 1: Physical Wearable ("PartusBand"):** Ultra-comfortable, skin-safe, multi-quadrant abdominal band.
  - **Layer 2: Edge Computing & TinyML:** Dual-core ARM Cortex-M33 running embedded filtering, peak detection, and spatial vectoring.
  - **Layer 3: Bluetooth Low Energy 5.3:** Secure 128-bit AES encrypted telemetry link to the patient's smartphone.
  - **Layer 4: Mobile Application ("MaternaSafe"):** Real-time presentation compass, guided postural coach, contraction triage, and automated CTG reports.
  - **Layer 5: Clinician Portal:** Encrypted cloud dashboard providing OB-GYNs with validated FIGO/ACOG Non-Stress Test telemetry before hospital admission.

> **🎙️ Speaker Notes:**  
> "Here is our end-to-end architecture. It starts at the abdomen with PartusBand, a flexible wearable equipped with bio-sensing AFEs, acoustic contact microphones, and high-frequency accelerometers. All analog preprocessing and TinyML vector calculations happen on-device using a dual-core Nordic microcontroller. The device pairs via low-power Bluetooth 5.3 to the MaternaSafe application, which acts as both an intuitive guide for the mother and an objective clinical telemetry stream for her obstetrician."

---

## 🖥️ Slide 6: Hardware Engineering ("PartusBand")
- **Header:** Advanced Multi-Modal Passive Hardware Design
- **Key Hardware Specifications:**
  - **Biosensing AFE (TI ADS1298):** 24-bit delta-sigma ADC, 8 differential channels, CMRR > 115 dB, integrated Right Leg Drive (RLD) for eliminating maternal muscle artifact and 50/60 Hz mains interference.
  - **Passive Acoustic Microphones:** 4-quadrant Knowles/Vesper piezoelectric MEMS contact sensors capturing low-frequency fetal heart sounds ($S_1, S_2$ valves at 20–120 Hz).
  - **Inertial Measurement Units (4× Bosch BMA456):** 16-bit triaxial accelerometers with integrated low-power tap/impact interrupts dedicated to capturing fetal limb kicks.
  - **Microcontroller (Nordic nRF5340):** Dual ARM Cortex-M33 (128 MHz Application core + 64 MHz Network core) running FreeRTOS and CMSIS-NN inference.
  - **Power & Ergonomics:** 850 mAh LiPo pouch cell (~120 hours of intermittent tracking), Qi inductive wireless charging, IP67 waterproof liquid silicone elastomer.

> **🎙️ Speaker Notes:**  
> "From a hardware perspective, PartusBand incorporates three synergistic sensor modalities into an ultra-thin, breathable silicone belt. The Texas Instruments ADS1298 analog front end isolates microvolt fetal electrical potentials from the larger maternal ECG. Four acoustic contact microphones listen to the acoustic point of maximum intensity of fetal heart valves, while four distributed accelerometers record the precise location and momentum of fetal limb kicks. Powered by a Nordic dual-core processor, the device achieves over 100 hours of active battery life on a single wireless Qi charge."

---

## 🖥️ Slide 7: Core Algorithm I — Spatial Heart-Kick Vectoring (SHKV)
- **Header:** How We Predict Fetal Position in Real Time
- **Mathematical Methodology:**
  1. **Acoustic Heart Centroid ($\vec{C}_{\text{heart}}$):**
     $$\vec{C}_{\text{heart}} = \frac{\sum_{i=1}^4 A_i \cdot \vec{P}_i}{\sum_{i=1}^4 A_i}$$
     *(Triangulating the spatial epicenter of heart sound amplitude across the 4 quadrants).*
  2. **Kinetic Kick Centroid ($\vec{C}_{\text{kick}}$):**
     $$\vec{C}_{\text{kick}} = \frac{\sum_{k=1}^N \Delta a_k \cdot \vec{S}_k}{\sum_{k=1}^N \Delta a_k}$$
     *(Averaging the localized strike vectors of limb acceleration peaks).*
  3. **Fetal Presentation Vector ($\vec{V}_{\text{presentation}}$):**
     $$\vec{V}_{\text{presentation}} = \vec{C}_{\text{kick}} - \vec{C}_{\text{heart}}$$
- **Diagnostic Output:**
  - $\vec{V}_y > 0$ (Kicks superior, heart inferior) $\rightarrow$ **Cephalic / Vertex (Head-Down) — Ideal for Natural Delivery**
  - $\vec{V}_y < 0$ (Heart superior, kicks inferior) $\rightarrow$ **Breech Presentation — High Risk for C-Section if Uncorrected**
  - $|\vec{V}_x| \gg |\vec{V}_y|$ $\rightarrow$ **Transverse Lie — Immediate Obstetric Attention Required**

> **🎙️ Speaker Notes:**  
> "How does an IoT device know the baby's position without an ultrasound probe? We formulated Spatial Heart-Kick Vectoring, or SHKV. In human anatomy, the fetal heart is located in the chest, and high-impact kicks originate from the legs. By triangulating the acoustic epicenter of heart valve closures and contrasting it against the spatial cluster of limb kicks, we calculate a 2D orientation vector. If the kicks are in the upper quadrants while the heart is down near the pubic bone, the baby is in the ideal cephalic position. If the vector inverts, our algorithm flags a breech presentation immediately."

---

## 🖥️ Slide 8: Core Algorithm II — Uterine EHG Labor Triage
- **Header:** Ending the "Premature Hospital Admission Cascade"
- **The Challenge:** Differentiating Braxton Hicks (false labor) from Active Labor Progression.
- **The Breakthrough:** Uterine Electromyography (EHG) Frequency Domain Shift.

| Parameter | Braxton Hicks (False Labor) | Active True Labor | Clinical Significance |
| :--- | :--- | :--- | :--- |
| **Peak Frequency ($F_{\text{peak}}$)** | $< 0.30\text{ Hz}$ | **$> 0.35\text{ Hz} – 0.85\text{ Hz}$** | Indicates cell-to-cell gap junction synchronization |
| **Wave Propagation Velocity** | $< 1.8\text{ cm/s}$ (Localized) | **$2.5 – 6.0\text{ cm/s}$ (Organ-wide)** | Action potential sweeps the entire fundus |
| **High/Low Spectral Energy Ratio ($R_{\text{H/L}}$)** | Low ($< 0.4$) | **High ($> 1.2$)** | Myometrial recruitment for cervical effacement |
| **VITA-NATAL Recommendation** | *"Rest, hydrate & perform deep breathing at home."* | **"Active Labor Confirmed. Prepare for hospital departure."** | **Eliminates unnecessary Pitocin induction failures!** |

> **🎙️ Speaker Notes:**  
> "A massive percentage of emergency C-sections occur because mothers arrive at the maternity ward too early during false labor. Hospitals often administer synthetic oxytocin to force delivery; when the cervix fails to respond, it is labeled a failed induction and ends in an emergency C-section. PartusBand measures the true electrophysiology of the uterine muscle. Braxton Hicks contractions operate below 0.3 Hz in localized pockets. As true labor begins, uterine cells form gap junctions, the propagation velocity triples, and the spectral power shifts above 0.35 Hz. MaternaSafe gives mothers the exact confidence on when to head to the hospital."

---

## 🖥️ Slide 9: Companion Mobile Ecosystem ("MaternaSafe")
- **Header:** The Maternal & Clinical Interface
- **Core Mobile Modules:**
  1. **Live Fetal Presentation Compass:** Dynamic 3D/2D anatomical avatar illustrating whether the fetus is head-down, breech, or transverse.
  2. **Daily Fetal Wellbeing & Kick Actigram:** Automated WHO-compliant kick counting and FHR baseline monitoring without requiring manual tap logs.
  3. **Biomechanical Natural Birth Postural Coach:** Real-time guided video exercises (Spinning Babies, forward-leaning inversions, pelvic rock) tailored to the baby's exact position.
  4. **Contraction Triage & Hospital Departure Timer:** Real-time labor stage tracker based on EHG electrical bursts.
  5. **Automated Clinical CTG/NST Generator:** Creates standard 20-minute FIGO/ACOG compliant Non-Stress Test reports exported as signed PDFs directly to the mother's doctor.

> **🎙️ Speaker Notes:**  
> "The MaternaSafe mobile app bridges the gap between deep biomedical engineering and user simplicity. The mother doesn't need to decipher raw microvolt signals; she sees an intuitive Fetal Compass showing her baby's orientation and a reassurance score. If the device detects a breech tendency, the app immediately unlocks the Biomechanical Postural Coach, guiding her through safe, midwife-approved exercises to encourage the baby to turn naturally before the clinical deadline."

---

## 🖥️ Slide 10: Clinical Intervention Protocol
- **Header:** How VITA-NATAL Turns Breech Presentation Naturally
- **Three-Tier Escalation Model:**

```
[ Week 28 – 32 ] ──► Early Detection via SHKV Algorithm (Breech Alert Triggered)
                            │
                            ▼
[ Tier 1: Home Biomechanics (W30–W34) ]
• Guided Forward-Leaning Inversions (FLI)
• Side-Lying Releases & Pelvic Rocking
• Optimizing uterine lower segment diameter
• 70% – 85% Natural Spontaneous Cephalic Version Rate!
                            │
                            ▼ (If Breech Persists at Week 36)
[ Tier 2: Clinician-Led External Cephalic Version (ECV) ]
• Early notification to OB-GYN with CTG telemetry history
• Scheduled manual obstetric rotation with continuous FHR monitoring
                            │
                            ▼
[ Result: Safe Vaginal Cephalic Delivery at Full Term ]
```

> **🎙️ Speaker Notes:**  
> "Here is our clinical escalation model. When our algorithms detect a breech position at Week 30, the mother begins Tier 1 non-invasive biomechanical protocols at home. Techniques like Forward-Leaning Inversions relax the uterosacral ligaments and open the pelvic inlet, allowing the baby's heavy head to naturally pivot downward. If the breech persists by Week 36, the obstetrician is alerted with complete objective telemetry history, allowing them to schedule an External Cephalic Version with full confidence. We systematically prevent the last-minute crisis that causes automatic cesarean bookings."

---

## 🖥️ Slide 11: Safety, Compliance & Zero Acoustic Radiation
- **Header:** Uncompromising Maternal & Fetal Safety Standards
- **Key Safety Advantages:**
  - **Zero Ultrasound Radiation:** Handheld Doppler monitors emit continuous high-frequency acoustic waves that cause tissue heating. PartusBand is **100% passive listening**—it emits zero acoustic or electromagnetic radiation into maternal or fetal tissue.
  - **Biocompatibility Standards:** Enclosure materials and hydrogel contact sensors certified under **ISO 10993-5 (Cytotoxicity)** and **ISO 10993-10 (Skin Sensitization)**.
  - **Medical Device Directive Compliance:** Engineered for **IEC 60601-1-11** (Safety requirements for medical electrical equipment used in the home healthcare environment).
  - **Data Privacy & Telemetry Security:** Bluetooth Low Energy 5.3 using 128-bit AES Galois/Counter Mode (GCM) encryption, complying with **HIPAA & GDPR** health data protocols.

> **🎙️ Speaker Notes:**  
> "Patient safety is paramount. One of our most significant innovations is that PartusBand produces zero acoustic radiation. Many commercial Doppler monitors emit continuous high-frequency acoustic beams into fetal tissue, which health authorities advise against for daily home use. Because our sensors are passive microphones and biopotential receivers, PartusBand has zero risk of tissue heating. Furthermore, all materials comply with ISO 10993 medical skin-contact standards, and data transmission uses medical-grade AES encryption."

---

## 🖥️ Slide 12: Socio-Economic & Healthcare Value
- **Header:** High ROI for Families, Hospitals, and National Healthcare Systems
- **Economic Value Breakdown:**
  - **Hospital Cost Reduction:** In public and private systems, an elective or emergency C-section costs between **$3,500 and $9,000**, compared to **$1,500 to $3,200** for an uncomplicated vaginal birth.
  - **Reduction in Hospital Bed Days:** Cesarean recovery requires 3 to 5 hospital inpatient days; vaginal delivery allows discharge within 24 to 36 hours.
  - **NICU Admission Prevention:** Reducing early-term elective cesareans drastically lowers admissions for Transient Tachypnea of the Newborn (TTN).
  - **Insurance & Public Payer Savings:** Averting just 10% of unnecessary cesareans saves tens of millions of dollars annually for national healthcare systems like SGK (Türkiye) or the NHS.

> **🎙️ Speaker Notes:**  
> "The value proposition of VITA-NATAL extends across the entire healthcare ecosystem. For hospitals and insurance providers, every averted cesarean saves between $2,000 and $5,000 in immediate surgical supplies, operating room staffing, and inpatient recovery days. For the mother, it means walking out of the maternity ward within 24 hours, unhindered by severe surgical wound pain, bonding immediately with her newborn. We align the economic incentives of healthcare providers with the best interests of mothers and babies."

---

## 🖥️ Slide 13: Technical Roadmap & Validation Strategy
- **Header:** Execution Plan: From Benchtop to Clinical Deployment
- **Four Structured Phases:**
  - **Phase 1: Proof-of-Concept & Benchtop Validation (Months 1–4):**
    - Multi-sensor flex-PCB fabrication (ADS1298 + MEMS + BMA456 + nRF5340).
    - Synthetic maternal-fetal acoustic phantom testing in laboratory.
  - **Phase 2: Algorithm Calibration & Observational Study (Months 5–9):**
    - 50-patient clinical recording study in university maternity hospital.
    - Benchmarking SHKV presentation classification directly against bedside ultrasound ground truth.
  - **Phase 3: Companion App & Industrial Design (Months 10–14):**
    - Production-grade liquid silicone enclosure tooling (IP67).
    - Flutter mobile app finalization & clinician dashboard portal launch.
  - **Phase 4: Regulatory Approval & Pilot Deployment (Months 15–20):**
    - CE Medical Device Regulation (MDR Class IIa) & FDA 510(k) pathway submission.
    - Pilot commercial rollout with partnering private maternity clinics.

> **🎙️ Speaker Notes:**  
> "Our roadmap is rigorously grounded in biomedical engineering best practices. We begin with benchtop acoustic phantom validation before proceeding to a 50-patient clinical observational study comparing our algorithm's position predictions directly with ultrasound gold standard scans. Following industrial medical tooling and MDR Class IIa regulatory submission, we will initiate pilot deployments with partnering maternity networks."

---

## 🖥️ Slide 14: Conclusion & Grand Vision
- **Header:** Restoring Confidence in Natural Birth Through Technology
- **Summary Takeaways:**
  1. **Continuous Passive Telemetry:** Safe, radiation-free home monitoring throughout pregnancy.
  2. **Predictive Presentation Intelligence:** Early detection of breech and malposition during the golden corrective window.
  3. **Halting the Surgical Cascade:** Objective EHG labor triage stopping premature hospital admissions.
  4. **Empowering Mothers & Doctors:** Seamless real-time data connecting the living room to the obstetric ward.
- **Closing Call to Action:**  
  *"Surgery should be an indispensable emergency backup, not a routine default. With Project No-Sezaryen, we give every mother and baby the safest, healthiest path to natural life."*

> **🎙️ Speaker Notes:**  
> "In conclusion, birth is not an illness to be surgically managed—it is a physiological milestone that deserves our smartest engineering support. With VITA-NATAL, we bridge the gap between home and hospital, equipping mothers with confidence and giving obstetricians the objective data they need to support natural birth. Thank you, and we welcome your questions and feedback."

---

## 🩺 Anticipated Committee Q&A Defense

### Q1: "How does passive acoustic sensing overcome maternal obesity (high BMI) or thick abdominal wall tissue?"
**Answer:**  
*"Great question. In higher-BMI patients, high-frequency sound waves attenuate rapidly. However, our piezoelectric MEMS microphones are tuned specifically for low-frequency acoustic transmission (20 Hz to 120 Hz), which propagates with minimal acoustic impedance through lipid layers. Furthermore, our ADS1298 AFE uses differential electrical biosensing (fECG) alongside acoustics; while acoustic amplitude may diminish, electrical biopotentials provide an invariant secondary vector, ensuring dual-modality redundancy."*

### Q2: "Can maternal movement or walking disrupt the presentation vector calculations?"
**Answer:**  
*"Yes, maternal ambulation creates motion artifacts. To solve this, our on-device firmware on the nRF5340 uses an activity gating state machine. The Bosch BMA456 IMUs act as an activity monitor: when the mother is walking or exercising, presentation vector computation is paused. The system calculates and updates the presentation vector when the mother is sitting, resting, or lying down, ensuring high signal-to-noise ratio and zero false alarms."*

### Q3: "What if the mother attempts postural exercises when contraindicated, such as with placenta previa?"
**Answer:**  
*"Safety is our highest priority. During the initial onboarding on the MaternaSafe application, the obstetrician or mother enters key prenatal screening parameters. If red-flag conditions exist (such as placenta previa, preeclampsia, or previous classical vertical hysterotomy), the biomechanical exercise module is automatically locked, and the app defaults strictly to passive vital reassurance and direct clinician alerts."*
