# ⚙️ Hardware & Embedded Subsystem Specifications
## Project No-Sezaryen (VITA-NATAL) Wearable Abdominal Tracker

---

## 1. System Block Diagram & Subsystem Partitioning

The physical tracker ("PartusBand") is architected as an ergonomic multi-sensor wearable device partitioned into three hardware domains:
1. **The Sensor Matrix Flexible Ribbon:** Embedded inside breathable, skin-conforming medical grade elastomer.
2. **The Central Processing & Telemetry Pod ("Core Pod"):** A lightweight, magnetically docked central unit containing the microcontrollers, wireless transceivers, and battery.
3. **The Power Management Subsystem (PMIC):** Wireless Qi-compliant charging with low-dropout regulators and high-efficiency buck converters.

```
+---------------------------------------------------------------------------------------+
|                             FLEXIBLE SENSOR MATRIX RIBBON                             |
|                                                                                       |
|  [Electrode RUQ]     [Acoustic Mic RUQ]    [IMU RUQ]       [Maternal Optical PPG]    |
|  [Electrode LUQ]     [Acoustic Mic LUQ]    [IMU LUQ]                                  |
|  [Electrode RLQ]     [Acoustic Mic RLQ]    [IMU RLQ]       [Skin Temperature Sensor]  |
|  [Electrode LLQ]     [Acoustic Mic LLQ]    [IMU LLQ]                                  |
+-------------------------------------------+-------------------------------------------+
                                            | High-Density FPC Connector
                                            v
+---------------------------------------------------------------------------------------+
|                                  CENTRAL POD (CORE PCB)                               |
|                                                                                       |
|   +-----------------------+     +-----------------------+     +-------------------+   |
|   |   ANALOG FRONT END    |     |   MCU & DSP ENGINE    |     |  WIRELESS MODEM   |   |
|   |  TI ADS1298 (fECG)    |---->| Nordic nRF5340 /      |---->| BLE 5.3 2.4 GHz   |   |
|   |  Quad Preamp (fPCG)   |     | ESP32-S3 (Dual-Core)  |     | Integrated PCB    |   |
|   |  I2C / SPI Bus Multiplex    | TinyML Inference      |     | Inverted-F Ant.   |   |
|   +-----------------------+     +-----------------------+     +-------------------+   |
|                                             ^                                         |
|                                             |                                         |
|                                 +-----------+-----------+                             |
|                                 |   POWER & BATTERY     |                             |
|                                 | TI BQ25120A PMIC      |                             |
|                                 | 850 mAh LiPo (3.7V)   |                             |
|                                 | Qi Wireless Receiver  |                             |
|                                 +-----------------------+                             |
+---------------------------------------------------------------------------------------+
```

---

## 2. Sensor Component Selection & Technical Rationale

### A. Electrophysiological AFE (fECG & EHG)
- **Primary IC:** **Texas Instruments ADS1298**
  - **Resolution:** 24-bit Delta-Sigma ADC.
  - **Channels:** 8 low-noise differential channels (simultaneous sampling).
  - **Input Referred Noise:** $4 \, \mu\text{V}_{\text{RMS}}$ (150 Hz BW).
  - **Common-Mode Rejection Ratio (CMRR):** $-115 \text{ dB}$ (crucial for rejecting 50/60 Hz mains interference).
  - **Integrated Features:** Right Leg Drive (RLD) amplifier, lead-off detection, internal reference voltage ($2.4 \text{ V}$).
  - **Electrode Material:** Dry conductive silicone with Ag/AgCl coating, eliminating gel irritation during prolonged wear.

### B. Acoustic Phono-Auscultation Array (fPCG)
- **Primary Transducer:** **Vesper VM3000** or **Knowles SPH0645LM4H-B** (or Piezoelectric PVDF Film Discs)
  - **Acoustic Bandwidth:** $10 \text{ Hz} – 300 \text{ Hz}$ tailored for deep mechanical heart acoustics.
  - **Signal-to-Noise Ratio (SNR):** $>65 \text{ dB(A)}$.
  - **Mechanical Coupling:** Acoustic silicone impedance-matching dome ensuring acoustic energy transfers directly from maternal skin into the sensor without ambient room noise.

### C. Fetal Kick & Actigraphy IMU Matrix
- **Primary IC:** **Bosch Sensortec BMA456** (4 units, 1 per quadrant)
  - **Type:** 16-bit ultra-low power triaxial accelerometer.
  - **Current Consumption:** $14 \, \mu\text{A}$ in low-power operational mode.
  - **Feature Engine:** On-chip interrupt generation for shock/tap events above programmable acceleration thresholds ($>0.08 \text{ g}$ impulse threshold), offloading the main MCU from continuous sampling.

---

## 3. Microcontroller & Computational Architecture

| Parameter | Specification | Engineering Benefit |
| :--- | :--- | :--- |
| **Processor** | **Nordic nRF5340** (Dual-Core ARM Cortex-M33) | Dedicated 128 MHz Application core for DSP/TinyML; dedicated 64 MHz Network core for BLE stack. |
| **DSP Support** | ARM Cortex-M33 with DSP instructions & Single-Precision FPU | Fast execution of Fast Fourier Transforms (FFT) and Finite Impulse Response (FIR) filtering. |
| **Flash / RAM** | 1 MB Flash / 512 KB RAM | Accommodates on-device TinyML neural network weights and raw buffer windows. |
| **Wireless Protocol** | Bluetooth 5.3 Low Energy (Long Range Coded PHY) | Penetrates domestic environments up to 50 meters with minimal transmission power ($+3 \text{ dBm}$). |
| **Hardware Cryptography** | ARM TrustZone & CryptoCell-312 | AES-128 / AES-256 hardware encryption of maternal medical streams over the air. |

---

## 4. Power Management & Battery Lifespan

### Current Consumption Budget

| Subsystem | State | Current Draw | Operational Duty Cycle |
| :--- | :--- | :--- | :--- |
| **ADS1298 AFE** | Active continuous 8-ch | $3.2 \text{ mA}$ | 100% |
| **4× MEMS Mics** | Active auscultation | $1.6 \text{ mA}$ | 100% |
| **4× BMA456 IMUs** | Low-power kick detect | $0.06 \text{ mA}$ | 100% |
| **nRF5340 App Core** | TinyML inference & filtering | $4.8 \text{ mA}$ | 25% (Burst execution) |
| **nRF5340 Net Core** | BLE sync (Connection int. 50ms)| $1.8 \text{ mA}$ | 10% |
| **Quiescent / Regulators**| Static leakage | $0.15 \text{ mA}$ | 100% |
| **Average Current** | **Continuous Mixed Tracking** | **$\approx 6.5 \text{ mA}$** | — |

- **Battery Capacity:** $850 \text{ mAh}$ ($3.7 \text{ V}$ LiPo).
- **Theoretical Operating Time:** $\frac{850 \text{ mAh}}{6.5 \text{ mA}} \approx 130.7 \text{ hours}$ (Standby/Sleep mode), or **$\approx 24–36 \text{ hours}$** of active continuous high-throughput data telemetry.
- **Wireless Charging:** Integrated Qi-compliant receiver coil (TI BQ51013B) charges the unit fully in $<1.5 \text{ hours}$ without external metallic charging ports.

---

## 5. Ergonomics, Enclosure & Skin Biocompatibility
- **Band Material:** Breathable medical-grade Lycra-silicone composite with hypoallergenic micro-perforations.
- **Enclosure:** Smooth injection-molded biocompatible polycarbonate (USP Class VI compliant).
- **Water Resistance:** IP67 sealed rating (withstands disinfectant wipes and perspiration).
- **Weight:** Central pod $<38 \text{ grams}$; total wearable band assembly $<95 \text{ grams}$.
