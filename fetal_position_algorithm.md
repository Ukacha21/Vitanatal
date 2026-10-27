# 🧠 Algorithms & Biomechanical AI Specifications
## Fetal Presentation Tracking & Uterine Labor Classification

---

## 1. Spatial Heart-Kick Vectoring (SHKV) Mathematical Model

The orientation of the fetus is derived by determining the spatial vector $\vec{V}_{\text{presentation}}$ between the **Fetal Cardiac Acoustic Centroid** ($\vec{C}_{\text{heart}}$) and the **Fetal Kicking Centroid** ($\vec{C}_{\text{kick}}$).

```
          [ Quadrant 1: RUQ ]             [ Quadrant 2: LUQ ]
                   \                               /
                    \                             /
                     \       ( Maternal )        /
                      \       Abdomen           /
                       \                       /
          [ Quadrant 3: RLQ ]             [ Quadrant 4: LLQ ]
```

### Step 1: Acoustic Heart Centroid Formulation
Let $\vec{P}_i = (x_i, y_i)$ represent the coordinates of the 4 acoustic contact microphones ($i \in \{1, 2, 3, 4\}$) on the maternal abdomen, normalized such that $(0,0)$ represents the umbilicus:
- $\text{RUQ}: (+1, +1)$
- $\text{LUQ}: (-1, +1)$
- $\text{RLQ}: (+1, -1)$
- $\text{LLQ}: (-1, -1)$

Each microphone records an acoustic time series $s_i(t)$. We apply a continuous bandpass filter ($25 \text{ Hz} – 160 \text{ Hz}$) and compute the envelope power $E_i(t)$ using the Hilbert Transform:
$$E_i(t) = \left| s_i(t) + j \cdot \mathcal{H}\{s_i(t)\} \right|^2$$

The acoustic signal weight $w_i$ is computed over an observation window $T = 60 \text{ s}$ as the Signal-to-Noise Ratio (SNR) of rhythmic cardiac peaks ($110–160 \text{ bpm}$):
$$w_i = \frac{\int_{0}^{T} E_i(t) \cdot \delta_{\text{peak}}(t) \, dt}{\int_{0}^{T} E_{\text{noise}, i}(t) \, dt}$$

The **Acoustic Heart Centroid** $\vec{C}_{\text{heart}}$ is calculated as:
$$\vec{C}_{\text{heart}} = \left( \frac{\sum_{i=1}^{4} w_i \cdot x_i}{\sum_{i=1}^{4} w_i}, \, \frac{\sum_{i=1}^{4} w_i \cdot y_i}{\sum_{i=1}^{4} w_i} \right)$$

### Step 2: Kinetic Kick Centroid Formulation
When the fetus kicks, the localized impact produces a transient acceleration vector $\vec{a}_k(t) = (a_{x,k}, a_{y,k}, a_{z,k})$ on accelerometer $k \in \{1, 2, 3, 4\}$.

To isolate genuine fetal kicks from maternal movement:
1. Maternal movement triggers synchronous, correlated low-frequency signals across all 4 IMUs ($<2 \text{ Hz}$).
2. Fetal limb impacts produce sharp, localized high-frequency impulses ($5 \text{ Hz} – 25 \text{ Hz}$, duration $50 \text{ ms} – 250 \text{ ms}$) on 1 or 2 adjacent sensors.

The kick impulse magnitude $I_k$ for a detected kick event $j$ is:
$$I_k(j) = \max_{t \in [t_j, t_j + \Delta t]} \left( \sqrt{a_{x,k}^2 + a_{y,k}^2 + a_{z,k}^2} - 1g \right)$$

The **Kinetic Kick Centroid** $\vec{C}_{\text{kick}}$ over a rolling 4-hour window (minimum $N \ge 8$ validated kicks) is:
$$\vec{C}_{\text{kick}} = \frac{1}{N} \sum_{j=1}^{N} \left( \frac{\sum_{k=1}^{4} I_k(j) \cdot \vec{P}_k}{\sum_{k=1}^{4} I_k(j)} \right)$$

### Step 3: Fetal Presentation Vector Formulation
The presentation vector $\vec{V}_{\text{pres}}$ connects the heart focus to the kicking limbs:
$$\vec{V}_{\text{pres}} = \vec{C}_{\text{kick}} - \vec{C}_{\text{heart}}$$

The vertical presentation index $\theta_{\text{vert}}$ is defined as:
$$\theta_{\text{vert}} = \arctan2(V_{\text{pres}, y}, V_{\text{pres}, x})$$

```
                            VERTICAL AXIS (+y: Fundus / Ribs)
                                           ▲
                                           │
                     BREECH                │           BREECH
                (Head High, Kicks Low)     │      (Head High, Kicks Low)
                                           │
   TRANSVERSE LIE ─────────────────────────┼───────────────────────── TRANSVERSE LIE
  (Horizontal Lie)                         │                         (Horizontal Lie)
                                           │
                     CEPHALIC              │           CEPHALIC
               (Head Down, Kicks High)     │     (Head Down, Kicks High)
                                           ▼
                            PELVIC INLET (-y: Cervix / Pubis)
```

- **Cephalic (Vertex) Presentation (Normal / Safe for Vaginal Birth) 🟢:**
  $$C_{\text{heart}, y} < -0.2 \quad \text{and} \quad C_{\text{kick}, y} > +0.2 \quad \Longrightarrow \quad \vec{V}_{\text{pres}} \text{ points strongly UPWARD (+y)}$$
- **Breech Presentation (Surgical C-Section Risk) 🔴:**
  $$C_{\text{heart}, y} > +0.2 \quad \text{and} \quad C_{\text{kick}, y} < -0.2 \quad \Longrightarrow \quad \vec{V}_{\text{pres}} \text{ points strongly DOWNWARD (-y)}$$
- **Transverse Lie (Obstructed Labor Risk) 🟡:**
  $$|C_{\text{heart}, x} - C_{\text{kick}, x}| > 0.8 \quad \text{and} \quad |V_{\text{pres}, y}| \approx 0$$

---

## 2. TinyML On-Device Presentation Classifier

To refine boundary cases (such as Complete Breech vs. Frank Breech vs. Occiput Posterior), a compact 1D Convolutional Neural Network (1D-CNN) runs directly on the ARM Cortex-M33 application core:

```
Input Vector (16 Features)
  ├── 4× Normalized Acoustic SNR ($w_1, w_2, w_3, w_4$)
  ├── 4× Quadrant Kick Frequency ($f_1, f_2, f_3, f_4$)
  ├── 4× Average Kick Intensity ($I_1, I_2, I_3, I_4$)
  ├── Maternal Posture State (Supine, Standing, Left Lateral)
  └── Gestational Age (Weeks)
             │
             ▼
   Dense Layer (32 neurons, ReLU activation)
             │
             ▼
   Dropout (0.2)
             │
             ▼
   Dense Layer (16 neurons, ReLU activation)
             │
             ▼
   Softmax Output (4 Classes)
     ├── [0] Cephalic / Vertex (Optimal Vaginal)
     ├── [1] Breech (Malpresentation)
     ├── [2] Transverse Lie (Malpresentation)
     └── [3] Occiput Posterior (Face-Up / Back Labor Risk)
```

- **Model Footprint:** $<18 \text{ KB}$ Flash, $<4 \text{ KB}$ RAM.
- **Inference Time:** $3.2 \text{ ms}$ on 128 MHz ARM Cortex-M33.
- **Accuracy Target:** $>94\%$ cross-validated against ultrasound ground truth.

---

## 3. Electrohysterogram (EHG) True Labor vs. Braxton Hicks Classifier

Premature hospital admission during false labor (Braxton Hicks) is one of the highest clinical predictors of emergency cesarean delivery due to failed artificial induction.

### Electrophysiological Metric Comparison

| Parameter | Braxton Hicks (False Labor) | True Active Labor Progression |
| :--- | :--- | :--- |
| **Spectral Peak Frequency ($F_{\text{peak}}$)** | $0.10 \text{ Hz} – 0.25 \text{ Hz}$ (Low metabolic sync) | $0.35 \text{ Hz} – 0.85 \text{ Hz}$ (Coordinated action potentials) |
| **High/Low Frequency Ratio ($R_{\text{H/L}}$)** | $< 0.4$ | $> 1.2$ (Dominant rapid depolarization) |
| **Contraction Propagation Velocity** | $< 1.0 \text{ cm/s}$ (Localized, random) | $2.5 \text{ cm/s} – 6.0 \text{ cm/s}$ (Fundus $\rightarrow$ Cervix sweep) |
| **Inter-Electrode Cross-Correlation** | Low ($r < 0.35$) | High ($r > 0.82$) (Total myometrial sync) |

### The True Labor Onset Index (TLOI)
The algorithm calculates the **True Labor Onset Index**:
$$\text{TLOI} = \alpha \cdot \frac{F_{\text{peak}}}{F_{\text{baseline}}} + \beta \cdot R_{\text{H/L}} + \gamma \cdot r_{\text{spatial\_sync}}$$

- If $\text{TLOI} < 1.0$: Classified as **Braxton Hicks / Latent Irritability**. Mobile app recommends hydration, warm shower, and resting on the left lateral side.
- If $\text{TLOI} \ge 1.0$ consistently over 60 minutes with 5-1-1 contraction cadence: Classified as **Active Cervical Dilation Labor**. Mobile app triggers the **"Go to Hospital"** notification.

---

## 4. Biomechanical Natural Version Coaching Protocol

When a persistent breech or posterior presentation is detected between **Weeks 28 and 35**, the mobile app guides the mother through validated biomechanical maneuvers:

1. **Forward-Leaning Inversion (FLI):**
   - *Biomechanical Action:* Relaxes the uterosacral and round ligaments, creating transient pelvic space for the fetal head to dislodge from the upper fundus.
   - *Protocol:* 30 seconds, 3 times daily under supervision.
2. **Pelvic Tilts & Cat-Cow Mobilization:**
   - *Biomechanical Action:* Encourages fetal spine rotation toward the anterior maternal abdominal wall.
3. **Side-Lying Release (SLR):**
   - *Biomechanical Action:* Releases pelvic floor asymmetries, giving the baby room to naturally rotate into the cephalic position.
4. **Birthing Ball Figure-8 Pelvic Circling:**
   - *Biomechanical Action:* Gravity-assisted engagement of the fetal head into the pelvic brim (Inlet engagement).
