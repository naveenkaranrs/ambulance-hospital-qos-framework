# Ambulance-to-Hospital Deterministic QoS Telemetry Framework 🚑

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Domain: Telemedicine](https://img.shields.io/badge/Domain-Emergency%20Telemedicine-blue)](https://github.com/naveenkaranrs)
[![Target: Embedded Gateway](https://img.shields.io/badge/Target-Embedded%20Gateway-0091BD)](https://github.com/naveenkaranrs)

An embedded network QoS scheduling framework designed for mobile emergency medical vehicles (ambulances) relaying continuous physiological telemetry to trauma centers over bandwidth-constrained, lossy cellular and mesh links.

---

## ⚡ Problem Formulation

In transit emergency medicine, transmission dropouts or latency spikes in diagnostic telemetry (12-lead ECG, blood oxygenation, trauma vitals) can delay critical intervention preparations at receiving hospitals.

This framework introduces a **Weighted Deficit Round-Robin (WDRR)** traffic scheduler on embedded gateway nodes that guarantees sub-50ms latency for critical diagnostic packets while dynamically throttling secondary streams (video/environmental telemetry) during network degradation.

---

## 📊 QoS Traffic Class Hierarchy

| Class ID | Stream Type | Strict Deadline | Priority Weight | Backoff Policy |
| :---: | :--- | :---: | :---: | :--- |
| **0x01** | Defibrillator / 12-Lead ECG Waveforms | < 50 ms | **10** | Zero drop, immediate retransmit |
| **0x02** | Real-Time Blood Pressure & SpO2 | < 150 ms | **6** | Delta compression |
| **0x03** | Ambient Cabin Diagnostics & GPS | < 1000 ms | **2** | Decimation upon congestion |
| **0x04** | Paramedic Situational Video | Best-Effort | **1** | Dynamic resolution scaling |

---

## 🚀 Key Implementations

- **Priority Queue Ring Buffer:** Microsecond-calibrated memory pools with zero-copy packet insertion.
- **Channel Quality Estimator:** Real-time round-trip latency & packet loss evaluation adjusting transmission rates.
- **Fail-Safe Offline Spooler:** Flash-backed circular journal preserving patient record integrity during total cellular blackouts.

---

## 📄 License
Released under the [MIT License](LICENSE).
