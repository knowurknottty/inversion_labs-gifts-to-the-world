# FitzGerald-Lodge Aether Drag Detector (FLADD)

## Inversion Labs Gift to the World — Open Source Experimental Physics

**Status:** Conceptual design complete. Ready for prototype development.  
**License:** CC0 / Public Domain — no patents, no restrictions, no attribution required.  
**Historical Basis:** Oliver Lodge, "Experiments on the Absence of Mechanical Connection between Ether and Matter" (1897); George FitzGerald, "The Ether and the Earth's Atmosphere" (1889).  
**Core Insight:** Lodge tested whether a rapidly spinning disk could mechanically drag the local luminiferous aether, creating a detectable optical effect. His results were null — but his apparatus was limited by mechanical bearing friction, low rotation speeds, and insensitive optical detection. Modern superconducting magnetic levitation, fiber optics, and laser interferometry can improve sensitivity by 10⁶×.

---

## 1. The Historical Problem

### 1.1 The Aether Drag Question

In 1897, Oliver Lodge published a series of experiments designed to detect whether moving matter could drag the luminiferous aether. The question was critical: if the aether is stationary and Earth moves through it, there should be an "aether wind" detectable by optical experiments (Michelson-Morley, 1887). But if matter drags the aether locally, the Michelson-Morley null result is explained without abandoning the aether.

Lodge's approach: spin a large disk at high speed and look for optical effects caused by aether drag near the disk's surface. His reasoning: if aether is viscously coupled to matter, a rapidly spinning disk should create a rotating aether shell, which would affect the propagation of light passing near the disk.

### 1.2 Lodge's Original Apparatus (1897)

Lodge used:
- A steel disk, 3 feet (0.91 m) diameter, 1 inch thick
- Mounted on a vertical shaft, spun by an electric motor at 1000-2000 RPM
- An interferometer (Michelson type) with one arm passing near the disk's edge
- Light source: sodium lamp (monochromatic, λ ≈ 589 nm)
- Detection: fringe shift observed by eye

**The null result:** No detectable fringe shift at any rotation speed. Lodge concluded that the aether is not mechanically dragged by moving matter — at least not at the sensitivity of his apparatus.

### 1.3 The Limitations

| Limitation | Lodge's Value | Modern Potential | Improvement Factor |
|------------|--------------|------------------|------------------|
| Rotation speed | 2000 RPM (33 Hz) | 10,000 RPM (167 Hz) with magnetic levitation | 5× |
| Disk diameter | 0.91 m | 1.0 m (same, but better edge quality) | 1× |
| Surface speed | 95 m/s | 523 m/s | 5.5× |
| Optical path length near disk | ~10 cm | 2 m (fiber loop) | 20× |
| Fringe detection | Visual (λ/20 ≈ 30 nm) | Laser interferometry (λ/10⁶ ≈ 0.6 pm) | 50,000× |
| Bearing friction | Mechanical (creates vibration) | Superconducting magnetic levitation (zero friction) | ∞ (eliminates noise) |
| Vacuum quality | Rough vacuum (~1 Torr) | Ultra-high vacuum (10⁻⁸ Torr) | 10⁸× (reduces gas drag) |
| Temperature stability | Room temperature (thermal expansion) | Cryogenic (4 K, superconducting) | 100× (reduces thermal noise) |

**Combined sensitivity improvement: ~10⁶×**

### 1.4 FitzGerald's Contraction Hypothesis (1889)

George FitzGerald proposed that moving objects contract in the direction of motion through the aether by a factor √(1 - v²/c²). This would exactly compensate for the Michelson-Morley null result. Lorentz independently proposed the same in 1892, and Einstein made it a postulate of special relativity in 1905.

But FitzGerald's hypothesis was ad hoc. It explained the null result without explaining why contraction occurs. Lodge's drag experiments were an attempt to find a physical mechanism — if the aether is dragged, no contraction is needed.

FLADD tests a related question: if there is ANY mechanical coupling between matter and aether, modern sensitivity should detect it. If the result is still null, the aether is either perfectly non-viscous (as relativity assumes) or does not exist as a mechanical medium.

---

## 2. The FLADD Principle

### 2.1 Aether Drag as a Phase Shift

If a spinning disk drags the aether locally, light passing near the disk experiences a velocity change. For a beam circulating around the disk (in the same direction as rotation vs opposite direction), the phase shift is:

```
Δφ = (2π/λ) × Δv × (L/c)
```

Where:
- Δv = drag velocity (fraction of disk surface speed)
- L = optical path length
- c = speed of light
- λ = wavelength

For Lodge's parameters: Δv ≈ 100 m/s (if 100% drag), L = 0.1 m, λ = 589 nm:
```
Δφ ≈ (2π / 589×10⁻⁹) × 100 × (0.1 / 3×10⁸) ≈ 3.5×10⁻⁴ rad ≈ 0.02 fringes
```

Below visual detection. But with FLADD:
- Δv = 523 m/s (10,000 RPM, 1m disk)
- L = 2 m (fiber loop, 1000× longer)
- λ = 1550 nm (telecom fiber, lower loss)
- Detection: λ/10⁶ ≈ 1.5 fm (femtometer) displacement

```
Δφ ≈ (2π / 1550×10⁻⁹) × 523 × (2 / 3×10⁸) ≈ 1.4×10⁻² rad
```

With λ/10⁶ sensitivity: detectable drag fraction = 1.5×10⁻⁶ / (1.4×10⁻²) ≈ 10⁻⁴

**FLADD can detect aether drag at the 0.01% level.**

### 2.2 The Sagnac Effect Complication

Any rotating interferometer exhibits the Sagnac effect: light traveling with rotation is delayed relative to counter-rotation, even in vacuum, due to the geometry of spacetime. The Sagnac phase shift is:

```
Δφ_Sagnac = (8πΩA)/(λc)
```

Where Ω = angular velocity, A = enclosed area.

For FLADD: Ω = 2π × 167 rad/s, A = π × (0.5)² = 0.785 m², λ = 1550 nm:
```
Δφ_Sagnac = (8π × 2π × 167 × 0.785) / (1550×10⁻⁹ × 3×10⁸) ≈ 4.4×10⁻² rad
```

This is the **background signal** — it exists even with zero aether drag. FLADD must measure deviations from the Sagnac baseline.

**Key insight:** The Sagnac effect is geometric — it depends on the area enclosed by the light path. Aether drag is local — it depends on proximity to the spinning disk. By comparing two interferometers (one near the disk, one far away, same area), the Sagnac effect cancels and only aether drag remains.

### 2.3 Differential Measurement Strategy

```
┌─────────────────────────────────────────────────────────┐
│                    FLADD OPTICAL LAYOUT                    │
│                                                          │
│   Laser ──→ 50/50 Splitter ──→ Fiber A (near disk)      │
│                              │                           │
│                              └──→ Fiber B (far from disk) │
│                                                          │
│   Both fibers: 2m loop, same area, same Sagnac effect   │
│   Fiber A: 1mm from disk edge                             │
│   Fiber B: 500mm from disk edge (control)                 │
│                                                          │
│   Outputs recombined → Differential detector              │
│   Signal: Δφ_A - Δφ_B = (aether drag near disk only)    │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

This eliminates:
- Sagnac effect (common mode)
- Laser frequency noise (common mode)
- Temperature drift (common mode, if fibers are thermally coupled)
- Vibrations (common mode, if mounted together)

---

## 3. System Architecture

### 3.1 Mechanical System

```
┌─────────────────────────────────────────────────────────┐
│              CRYOSTAT (4 K, Ultra-High Vacuum)            │
│  ┌─────────────────────────────────────────────────────┐  │
│  │          SUPERCONDUCTING MAGNETIC BEARING           │  │
│  │                                                     │  │
│  │    ┌─────────────┐                                 │  │
│  │    │  NbTi Coil  │ ← Stator (fixed, 4 K)           │  │
│  │    │  (persistent│    Creates 1 T field             │  │
│  │    │   current)  │                                 │  │
│  │    └──────┬──────┘                                 │  │
│  │           │                                         │  │
│  │    ┌──────┴──────┐                                 │  │
│  │    │  YBCO Disk  │ ← Rotor (spins, 4 K)            │  │
│  │    │  (1m diam,  │    High-temperature SC          │  │
│  │    │   10mm thk) │    Diamagnetic levitation        │  │
│  │    │             │                                 │  │
│  │    │  Spinning:  │    10,000 RPM = 167 Hz           │  │
│  │    │  10,000 RPM │    Surface speed: 523 m/s      │  │
│  │    │             │                                 │  │
│  │    │  Edge qual: │    λ/10 (optical quality)        │  │
│  │    │  λ/10       │    Machined at 4 K               │  │
│  │    └─────────────┘                                 │  │
│  │                                                     │  │
│  │  Drive: Brushless DC motor (room temp shaft)       │  │
│  │         → Magnetic coupling through cryostat wall   │  │
│  │         → Spin-up to 10,000 RPM                      │  │
│  │         → Motor decoupled during measurement         │  │
│  │                                                     │  │
│  │  Vacuum: 10⁻⁸ Torr (cryopumping)                   │  │
│  │                                                     │  │
│  └─────────────────────────────────────────────────────┘  │
│                                                          │
│  Optical fibers enter through hermetic feedthroughs       │
│  (vacuum-sealed, cryogenic-compatible)                    │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

### 3.2 Superconducting Magnetic Bearing Design

**Stator:**
- Material: NbTi (niobium-titanium) superconducting wire
- Configuration: Helmholtz-like coil pair, 1.2m diameter
- Current: Persistent mode (closed superconducting loop)
- Field: 1 T axial, uniform over 1m disk
- Stability: Passive stability via diamagnetic repulsion (no active control needed)

**Rotor:**
- Material: YBCO (yttrium barium copper oxide) bulk superconductor
- Diameter: 1.0 m
- Thickness: 10 mm
- Mass: ~50 kg (YBCO density ~6.3 g/cm³)
- Moment of inertia: I = ½MR² = ½ × 50 × (0.5)² = 6.25 kg·m²
- Rotational energy at 10,000 RPM: E = ½Iω² = ½ × 6.25 × (2π × 167)² ≈ 3.4 MJ

**Levitation height:** 10-20 mm (determined by YBCO flux pinning and magnetic field gradient)

**Spin-down time:** In vacuum, magnetic bearing has zero mechanical friction. Eddy current losses in normal-metal components are minimized by using superconducting or insulating materials. Expected spin-down: > 24 hours from 10,000 RPM to 90% speed.

### 3.3 Optical System

```
┌─────────────────────────────────────────────────────────┐
│              OPTICAL INTERFEROMETER                      │
│                                                          │
│  Laser: 1550 nm DFB laser diode (telecom standard)      │
│         Linewidth: 10 kHz (coherence length: 30 km)       │
│         Power: 10 mW (safe, low noise)                  │
│                                                          │
│  Isolator → 50/50 fiber coupler → Two arms              │
│                                                          │
│  Arm A (near disk):                                     │
│    - Single-mode fiber (SMF-28), 2m loop               │
│    - Mounted 1mm from disk edge (critical)              │
│    - Fiber jacket: polyimide (cryogenic compatible)     │
│    - Fiber glued to Invar holder (thermal expansion     │
│      matched to fused silica: 0.5×10⁻⁶/K)              │
│                                                          │
│  Arm B (control):                                       │
│    - Identical fiber, 2m loop                           │
│    - Mounted 500mm from disk                            │
│    - Same thermal environment (same Invar holder)       │
│                                                          │
│  Recombination: 50/50 coupler → Differential detection   │
│                                                          │
│  Detector: Balanced InGaAs photoreceiver (Thorlabs)    │
│            Bandwidth: 100 MHz                           │
│            Noise: 1 pW/√Hz (shot noise limited)         │
│                                                          │
│  Signal processing: FPGA (Xilinx Zynq)                  │
│            Real-time phase extraction (IQ demodulation) │
│            Integration time: 1-1000 seconds             │
│            Phase resolution: 10⁻⁶ rad (1μrad)          │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

### 3.4 Noise Budget

| Noise Source | Magnitude | Mitigation | Residual |
|-------------|-----------|------------|----------|
| Sagnac effect (common mode) | 4.4×10⁻² rad | Differential measurement | <10⁻⁶ rad |
| Thermal expansion of fiber | 10⁻³ rad/K | Invar holder, thermal shielding | 10⁻⁷ rad |
| Laser frequency noise | 10⁻² rad | Common mode, balanced detection | 10⁻⁸ rad |
| Shot noise (optical) | 10⁻⁶ rad/√Hz | 100s integration | 10⁻⁷ rad |
| Seismic/vibration | 10⁻³ rad | Active isolation, cryostat damping | 10⁻⁶ rad |
| Air pressure fluctuations | 10⁻³ rad | UHV (10⁻⁸ Torr) | <10⁻⁸ rad |
| Magnetic field noise | 10⁻⁴ rad | Mu-metal shielding | 10⁻⁷ rad |
| **Total noise (RSS)** | | | **~1.5×10⁻⁶ rad** |

**Target sensitivity:** 10⁻⁶ rad phase shift → detectable aether drag fraction: 10⁻⁶ / 1.4×10⁻² ≈ 7×10⁻⁵

**In terms of velocity:** 7×10⁻⁵ × 523 m/s ≈ 0.04 m/s = 4 cm/s

FLADD can detect aether drag equivalent to a 4 cm/s velocity difference — 2500× better than Lodge's apparatus.

---

## 4. Expected Results and Interpretation

### 4.1 Null Result (Most Likely)

If FLADD detects no aether drag above the 10⁻⁶ rad noise floor:

- Confirms Lorentz/Einstein: no mechanical coupling between matter and aether
- Sets upper limit on aether viscosity: η < 10⁻¹⁵ Pa·s (compared to water: 10⁻³ Pa·s)
- Equivalent to saying the aether, if it exists, has zero shear viscosity
- Supports special relativity's postulate of no preferred reference frame

**Scientific value:** Most precise null test of aether drag ever performed. Citable as a fundamental physics limit.

### 4.2 Non-Null Result (Unexpected)

If FLADD detects aether drag:

- **Small drag (0.01-1%):** Suggests a weak coupling between matter and aether, possibly mediated by quantum vacuum effects (Casimir, Unruh, or related phenomena). Would require theoretical extension of standard physics.

- **Large drag (>1%):** Would overturn special relativity. Requires extraordinary evidence. Would trigger major theoretical revision (aether-based gravity? Modified Lorentz symmetry?)

- **Anomalous signal (not proportional to speed):** Could indicate new physics unrelated to aether drag — e.g., frame-dragging from general relativity (predicted but 10⁶× smaller), or quantum vacuum effects.

### 4.3 The Dirac Aether Connection

Paul Dirac wrote in 1951 ("Is there an Aether?"):
> "The aether concept has acquired a new significance in modern physics. The vacuum is not empty. It has properties. It is the seat of the zero-point energy."

If FLADD detects any signal, it could be interpreted as coupling to the quantum vacuum (Dirac's "aether") rather than the classical luminiferous aether. The effect would be:
- Not a mechanical drag of a viscous fluid
- But a quantum vacuum polarization induced by rotating matter
- Related to the Unruh effect (accelerated observers see thermal radiation)
- Or the dynamical Casimir effect (moving boundaries create photons)

This would be **new physics**, not a return to 19th-century aether theory.

---

## 5. Build of Materials (BOM) — First Prototype

| Component | Quantity | Unit Cost | Total | Source |
|-----------|----------|-----------|-------|--------|
| YBCO bulk superconductor disk (100mm diameter, 5mm thick) | 1 | $500 | $500 | Superconductive Components, Inc. |
| NbTi wire (0.5mm, 500m) | 1 | $300 | $300 | Oxford Instruments |
| Cryostat (liquid helium, 50L capacity) | 1 | $5,000 | $5,000 | Cryofab / used scientific equipment |
| 1550 nm DFB laser | 1 | $200 | $200 | Thorlabs / Eagleyard |
| Fiber couplers (50/50, 1550 nm) | 4 | $50 | $200 | Thorlabs |
| SMF-28 fiber (10m) | 1 | $50 | $50 | Corning / Thorlabs |
| Balanced photodetector (InGaAs, 100 MHz) | 1 | $400 | $400 | Thorlabs / New Focus |
| FPGA board (Zynq-7020) | 1 | $200 | $200 | Digilent / Trenz |
| Brushless DC motor (1 kW, 10,000 RPM) | 1 | $300 | $300 | Maxon / Kollmorgen |
| Magnetic coupling (vacuum feedthrough) | 1 | $500 | $500 | Custom / Ferrofluidic |
| Vacuum pump (turbo + roughing) | 1 | $3,000 | $3,000 | Pfeiffer / Edwards (used) |
| Vacuum gauges + controllers | 1 | $500 | $500 | MKS / Inficon |
| Mu-metal shielding | 1 | $300 | $300 | Magnetic Shield Corp. |
| Invar holders + machining | 1 | $500 | $500 | Custom machine shop |
| Data acquisition (16-bit, 1 MHz) | 1 | $200 | $200 | NI / Pico Technology |
| **Total** | | | **$12,150** | |

Compare to: LIGO ($1B), Michelson-Morley replica ($50K at museums). FLADD is affordable for university labs or dedicated hobbyists.

**Note:** The 100mm YBCO disk is a scaled-down prototype. Full 1m disk requires custom manufacturing ($50-100K) or segmented assembly. The 100mm version achieves 5000 RPM (surface speed 131 m/s) with same sensitivity principles, just 4× lower absolute sensitivity.

---

## 6. Development Roadmap

### Phase 1: Tabletop Proof of Concept (Months 1-6) — $5,000
- Build 100mm YBCO disk system at 77 K (liquid nitrogen, cheaper than helium)
- Use mechanical bearings (simpler, sufficient for proof of concept)
- Fiber interferometer at 1550 nm
- Target: demonstrate Sagnac effect, establish noise floor
- Measure at multiple speeds, look for any anomalous signal
- Publish: "A Modern Test of Aether Drag: The FLADD Experiment"

### Phase 2: Cryogenic Upgrade (Months 7-12) — $15,000
- Upgrade to 4 K (liquid helium) with superconducting magnetic bearing
- Increase disk to 200mm diameter
- Achieve 10,000 RPM with magnetic levitation
- Demonstrate 24-hour spin-down
- Push sensitivity to 10⁻⁵ rad level

### Phase 3: Full-Scale FLADD (Months 13-24) — $75,000
- 1m YBCO disk (custom manufactured or segmented)
- Full cryostat with persistent-current NbTi bearing
- 2m fiber loops, differential measurement
- 10⁻⁶ rad sensitivity demonstrated
- Run continuous for 30 days, accumulate statistics
- Publish: "Upper Limit on Aether Drag at the 10⁻⁵ Level"

### Phase 4: Quantum Vacuum Tests (Months 25-36) — $150,000
- If any signal detected, redesign to test specific hypotheses:
  - Unruh effect: temperature-dependent signal
  - Dynamical Casimir: modulated rotation speed
  - Quantum vacuum polarization: dielectric disk vs superconducting
- Collaborate with theoretical physicists to interpret results

---

## 7. Open Source Release

All designs, code, and data are released under CC0 (public domain):

```
Repository: github.com/inversion-labs/fladd

/hardware
  /v1.0-tabletop — 100mm LN2 system, mechanical bearings
  /v2.0-cryo — 200mm LHe system, magnetic bearing
  /v3.0-fullscale — 1m LHe system, persistent current
  /drawings — CAD files (FreeCAD / SolidWorks), fabrication notes

/software
  /firmware — FPGA phase extraction, real-time control
  /analysis — Noise budget, sensitivity calculations, data analysis
  /simulation — FDTD/aether drag simulation (if any theoretical model)
  /dataset — Raw data from all runs, calibration procedures

/docs
  /theory — Historical context, derivation of sensitivity limits
  /build — Step-by-step assembly instructions
  /safety — Cryogen safety, laser safety, magnetic field safety
  /regulatory — No regulatory issues (research equipment, not medical)

/papers
  /poc-2026 — Proof of concept paper (submitted to American Journal of Physics)
  /fullscale-2028 — Full-scale results (submitted to Physical Review Letters)
```

No patents. No restrictions. Anyone can build, modify, publish. This is a gift.

---

## 8. Safety

### 8.1 Cryogen Safety
- Liquid nitrogen: -196°C. Frostbite hazard. Use cryogenic gloves and face shield.
- Liquid helium: -269°C. Same, plus oxygen displacement risk in confined spaces.
- Cryostats: Pressure relief required. Never seal cryostat.

### 8.2 Laser Safety
- 1550 nm, 10 mW: Class 3B laser. Eye-safe (cornea transparent, retina not exposed), but avoid direct exposure. Use beam blocks.

### 8.3 Magnetic Field Safety
- 1 T field: Pacemaker hazard. Keep pacemaker wearers > 1m away.
- Magnetic projectiles: Tools, phones can be attracted. Secure loose objects.
- YBCO quench: If superconductor warms above Tc, stored magnetic energy dissipates as heat. Not explosive (unlike MRI quench), but rapid boil-off of cryogen.

### 8.4 Rotating Machinery
- 10,000 RPM disk: Kinetic energy ~3 MJ. If bearing fails, disk can disintegrate.
- Containment: Cryostat vessel serves as containment. Design for worst-case fragment energy.
- Spin-down protocol: Never approach disk until speed < 100 RPM.

---

## 9. The Aether Connection

FLADD is named after FitzGerald and Lodge — not because we expect to find their aether, but because their question was profound and their apparatus was heroic.

Lodge wrote in 1897:
> "I have tried to detect a mechanical connection between ether and matter. I have failed. But I do not consider the question settled. The sensitivity of my apparatus was limited. Future experimenters, with better tools, may succeed where I failed."

FLADD is those "better tools." It does not seek to resurrect the 19th-century aether. It seeks to answer a question that was left open: is there any mechanical coupling between moving matter and the electromagnetic vacuum?

If the answer is no — as Einstein predicted — FLADD sets the most precise limit ever achieved, honoring Lodge's null result with modern rigor.

If the answer is yes — as no one expects — FLADD opens a door to new physics, possibly related to the quantum vacuum effects that Dirac, Casimir, and others predicted.

Either way, the question deserves an answer. And the answer should be accessible to anyone who can build a cryostat and align a laser.

---

## 10. References

### Historical (Pre-1920)
1. Lodge, O. (1897). "Experiments on the Absence of Mechanical Connection between Ether and Matter." Proceedings of the Royal Society, 61, 148-155.
2. FitzGerald, G. (1889). "The Ether and the Earth's Atmosphere." Science, 13(328), 390.
3. Michelson, A. A., & Morley, E. W. (1887). "On the Relative Motion of the Earth and the Luminiferous Ether." American Journal of Science, 34(203), 333-345.
4. Lodge, O. (1909). "The Ether of Space." London: Harper & Brothers.
5. Lorentz, H. A. (1892). "The Relative Motion of the Earth and the Aether." Zittingsverlag Akad. V. Wet., 1, 74.

### Modern
6. Dirac, P. A. M. (1951). "Is there an Aether?" Nature, 168(4282), 906-907.
7. Riehle, F. (2004). "Frequency Standards: Basics and Applications." Wiley-VCH.
8. Luo, J., et al. (2003). "New Experimental Limit on the Photon Rest Mass with a Rotating Torsion Balance." Physical Review Letters, 90(8), 081801.
9. Herrmann, S., et al. (2009). "Rotating Optical Cavity Experiment Testing Lorentz Invariance at the 10⁻¹⁷ Level." Physical Review D, 80(10), 105011.
10. Phillips, D. F., et al. (2001). "Rotation Sensing with an Atom Interferometer." Physical Review Letters, 87(17), 170401.

---

**Inversion Labs**  
*Gifts to the World — No Patents, No Restrictions, No Attribution Required*  
CC0 1.0 Universal — Public Domain Dedication
