# CHORUS Orator

**Real-time voice analysis and cognitive state detection using 8 acoustic channels.**

CHORUS (Composite Harmonic Orator Recognition and Understanding System) listens to your voice through the microphone and builds a live **phase atlas** — a circular map where time sweeps clockwise and 8 concentric rings represent different acoustic dimensions of your speech.

It computes two science-backed scores in real time — **Cognitive Load** and **Stress** — and determines a dominant cognitive state: **Focused**, **Stressed**, **Processing**, **Fatigued**, or **Guarded**.

All comparisons are to **your own baseline**, not population norms. Different speakers have different ranges — CHORUS adapts to you.

---

## Live Demo

**[Launch CHORUS Orator →](https://hussein-marouf.github.io/chorus-orator/)**

Requires microphone access. Works best in Safari (iOS) or Chrome/Firefox (desktop).

---

## The 8 Acoustic Channels

| Ring | Channel | Color | What It Measures |
|------|---------|-------|-----------------|
| 1 (inner) | **Loudness** | 🔴 Red | RMS intensity relative to calibrated noise floor |
| 2 | **Pitch** | 🟠 Orange | Fundamental frequency (F0) via autocorrelation |
| 3 | **Rate** | 🟢 Green | Syllable rate from envelope peak detection |
| 4 | **Pauses** | 🔵 Cyan | Silence density within a 3-second window |
| 5 | **Brightness** | 🟣 Purple | Spectral centroid — correlates with arousal |
| 6 | **Stability** | 🟡 Yellow | Inverse jitter — pitch-to-pitch perturbation |
| 7 | **Clarity** | 🔵 Blue | Harmonics-to-noise proxy via autocorrelation confidence |
| 8 (outer) | **Texture** | 🩷 Pink | Zero-crossing rate — breathiness vs voicing |

---

## Cognitive State Detection

CHORUS computes 5 state scores simultaneously and reports the dominant one:

- **FOCUSED** — Low cognitive load, stable voice, good clarity. The speaker is calm and engaged.
- **STRESSED** — Elevated F0 and intensity above baseline, spectral shift upward, clarity degrading. Physiological arousal markers.
- **PROCESSING** — High mental effort. Pitch variance increases, rate decreases, pauses increase, fluency drops. This is the cognitive load signature — the same pattern associated with information management, complex reasoning, or deception.
- **FATIGUED** — Reduced intensity, pitch, and rate. Monotone delivery with diminished vocal dynamics.
- **GUARDED** — Elevated F0 combined with increased F0 variance, more pauses, slower rate, and reduced clarity. The multi-channel signature associated with information management and concealment in peer-reviewed literature.

State transitions require **12 consecutive frames** (0.4 seconds) of agreement before switching, preventing flicker and ensuring stability.

---

## Scientific Basis

The core 4 channels (loudness, pitch, rate, pauses) are validated across 39+ studies in a [2025 PLOS One systematic review](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0328833). Prosodic features showed correlation with emotional and cognitive states in 75% of cases examined.

Key findings from the literature that inform CHORUS:

- **Stress** → increased F0 and intensity, reduced speech duration ([Kappen et al., 2024, *Scientific Reports*](https://www.nature.com/articles/s41598-024-55550-3))
- **Cognitive load** → slower speech rate, increased hesitation, prolonged pauses ([Yache et al., 2025, *Frontiers in Psychiatry*](https://www.frontiersin.org/journals/psychiatry/articles/10.3389/fpsyt.2025.1656292/full))
- **Deception-adjacent patterns** → increased pitch variance, longer response latencies, slower tempo, reduced fluency, increased intensity range ([Hirschberg et al., 2020, *TACL*](https://direct.mit.edu/tacl/article/doi/10.1162/tacl_a_00311/43547))

CHORUS labels these patterns honestly — **Processing** and **Guarded** rather than "lying" — because audio-only deception detection tops out at ~68% accuracy in controlled conditions. The cognitive load signal is real; the interpretation is the user's.

---

## Features

- **Phase Atlas** — Circular visualization where time sweeps clockwise at 8°/second. Bright rings = active channels. Dark = quiet.
- **Radar Sweep** — 35° dark wipe ahead of the needle clears old data so you always see where "now" is.
- **12 O'Clock Label** — Large status word at top of atlas shows dominant cognitive state at a glance.
- **Interpretation Sentence** — Natural language explanation of what all 8 channels mean combined, updated 30 times per second.
- **Noise Floor Calibration** — 2-second silence calibration at startup learns your room's ambient noise.
- **Session Recording** — Record microphone audio as WebM and download.
- **Report Generation** — One-click HTML report with atlas snapshot, state timeline, channel averages, phase transitions, and peak scores.
- **100% Local** — No data transmitted. All analysis runs in the browser via Web Audio API.

---

## How to Use

1. Open the app and click **Begin**
2. Allow microphone access when prompted (or use Demo Mode)
3. Stay quiet for 2 seconds during calibration
4. Start speaking — the atlas builds in real time
5. Press **● Rec** to record audio, **Report** to download analysis

### On iPhone
Open in **Safari** (not Chrome). Tap Allow for microphone. Add to Home Screen for full-screen app experience.

---

## Technical Details

- **Analysis rate:** 30 Hz (33ms per frame)
- **FFT size:** 2048 samples
- **Pitch detection:** Autocorrelation with parabolic interpolation, range 70–500 Hz
- **Normalization:** Exponential moving average with 3-second tau, z-score relative to running statistics
- **Phase detection:** Zero-crossings of first derivative of weighted composite field S(t), with salience threshold and minimum 3-second phase duration
- **State debounce:** 12-frame (0.4s) hysteresis prevents flicker

---

## Disclaimer

CHORUS Orator is an acoustic analysis tool, not a diagnostic or forensic instrument. Cognitive state labels are based on validated prosodic markers from peer-reviewed speech science research, but reflect statistical tendencies across populations — not certainties about any individual. These readings should not be used for forensic, legal, medical, or employment decisions.

---

## Author

**Hussein Marouf** — Independent Researcher, Abacus Omega Inc.

---

## License

This work is licensed under [Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/).

You are free to share and adapt this work for non-commercial purposes, provided you give appropriate credit. For commercial licensing inquiries, contact the author.

© 2025 Hussein Marouf. All rights reserved for commercial use.
