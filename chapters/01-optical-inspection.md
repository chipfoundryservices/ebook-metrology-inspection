# Chapter 1: Optical Inspection Fundamentals

## The Diffraction Limit Barrier

When semiconductor fabs first adopted automated optical inspection (AOI) in the 1990s, the problem was simple: find dust particles and solder bridges on printed circuit boards. Optical microscopes work fine for that.

But at 28nm nodes (2011), defects became small. At 7nm (2018), invisible to light. At 3nm (2023), **optical inspection fails fundamentally.**

This chapter explains why—and why the industry is scrambling to replace optical inspection with e-beam metrology (which works at any wavelength).

---

## I. Inversion: What Destroys Optical Inspection?

### Failure 1: Diffraction Limit Below 200nm

The resolution of any optical system is bounded by diffraction:

```
Resolution = λ / (2 × NA)
```

Where:
- λ = wavelength of light (e.g., 365 nm for UV, 193 nm for deep-UV)
- NA = numerical aperture (~0.9 for modern lenses)

**At 193 nm wavelength:**
```
Resolution = 193 / (2 × 0.9) ≈ 107 nm
```

**At 365 nm wavelength:**
```
Resolution = 365 / (2 × 0.9) ≈ 200 nm
```

At 3nm nodes, defects are 10-50 nm in size. **Optical inspection cannot resolve them.**

### Failure 2: Contrast Degradation at Low Wavelength

Deep-UV (193 nm) light does not penetrate dielectrics deeply. It scatters in the oxide, creating noise. **Signal-to-noise ratio collapses.**

Defect contrast (defect reflectivity - background reflectivity) drops from 20% at 248 nm to 5% at 193 nm. **5% contrast is too noisy for automated detection.**

### Failure 3: Throughput vs. Resolution Trade-off

To achieve 50 nm resolution, optical systems must:
1. Use small field of view (reduces throughput)
2. Increase exposure time (reduces throughput further)
3. Use bright illumination (creates thermal issues)

**Result:** 1,000 wafers/month throughput (unacceptable for production).

E-beam metrology: 100-300 wafers/month (barely acceptable, but improving).

---

## II. Physics: Optical Inspection Principles

### A. Coherent vs. Incoherent Light Sources

**Coherent light (lasers):**
- All photons in phase → sharp diffraction patterns
- Interference creates speckle noise → false defect signals
- **Disadvantage:** Speckle makes interpretation ambiguous

**Incoherent light (LEDs, lamps):**
- Photons randomly phased → no speckle
- **Advantage:** Clean optical contrast
- **Disadvantage:** Lower intensity → longer exposure times

Modern AOI systems use **partially coherent light** (tunable coherence) to balance contrast and speckle.

### B. Bright-field vs. Dark-field Imaging

**Bright-field:**
- Light hits substrate, reflects straight back to camera
- High signal; good for general defects
- Poor for small isolated defects (low contrast)

**Dark-field:**
- Scattered light only (direct reflection blocked)
- Detects small particles and edges preferentially
- **Trade-off:** Higher contrast for defects, but lower overall signal

Most automated systems use **multi-spectral imaging:** bright-field + dark-field + different wavelengths (365 nm + 248 nm) to maximize defect detection.

### C. Lens Aberrations at High NA

High numerical aperture (NA ~0.9) introduces optical aberrations:
- Spherical aberration (off-axis rays don't focus at center)
- Coma (asymmetric blur off-axis)
- Astigmatism (different focus in x vs. y)

**Consequence:** Resolution varies across field of view. Edge of image is ~50% worse resolution than center.

Modern systems use **adaptive optics** (deformable mirrors) to correct aberrations in real time.

---

## III. Practice: AOI Equipment Design

### Automated Optical Inspection (AOI) System Architecture

**Key components:**

1. **Illumination:** Multi-wavelength LED array (365 nm, 248 nm, sometimes 632 nm)
2. **Optics:** High-NA lens (NA 0.9), possibly with adaptive optics
3. **Camera:** High-resolution CCD/CMOS (2 megapixels typical)
4. **Motion stage:** XY stage for wafer scanning, Z for focus
5. **Image processing:** Real-time defect detection algorithms
6. **Database:** Reference images, defect libraries, historical trends

### Throughput vs. Resolution

| Configuration | Resolution | Throughput | Use Case |
|---|---|---|---|
| High-res mode | 100-150 nm | 100 wafers/month | Sub-7nm nodes (post-lithography) |
| Medium-res mode | 150-250 nm | 300 wafers/month | 7nm-14nm node inspection |
| High-throughput mode | 250-400 nm | 1,000+ wafers/month | ≥28nm nodes |

**Fab decision:** Sub-3nm nodes require multiple passes at different resolutions. Total time: 8-12 hours per wafer (unacceptable for production-line speeds).

### Multi-spectral Approach

Modern AOI systems use multiple wavelengths simultaneously:

| Wavelength | Penetration | Defect Sensitivity |
|---|---|---|
| 365 nm (UV) | ~50 nm into oxide | Good for oxide defects |
| 248 nm (deep-UV) | ~20 nm into oxide | Best for thin oxide/metal defects |
| 632 nm (red) | ~1000 nm into oxide | Good for buried defect detection |

**Fabs run three separate passes** (365 nm, 248 nm, 632 nm) to maximize defect detection. This triples inspection time.

---

## IV. Economics: Why Optical Inspection Is Dying

### Capital Cost

**Typical AOI system:** $500K-$1.5M per tool

**Throughput:** 300-1,000 wafers/month (depending on resolution mode)

**Capex per wafer (in-steady state):** $50-200/wafer

**But here's the problem:** At 3nm nodes, fabs need **two AOI tools** (different resolution modes) just to achieve adequate defect detection. Cost doubles.

### Service Cost

- Maintenance: $50K-$100K/year
- Calibration/alignment: $30K/year
- Software updates: $20K/year
- **Total service cost:** $100-150K/year

### The Throughput Crisis

At sub-3nm nodes:
- Multi-spectral imaging required: 3 passes × 4 hours/pass = 12 hours/wafer
- Wafer throughput: 300 wafers / 12 hours = **25 wafers/hour max**

For a 50K wafers/month fab:
- Required AOI capacity: 50,000 / (25 wafers/hour × 160 hours/month) = **12.5 tools**
- Capex: 12.5 × $1M = **$12.5M just for AOI**

**This is unaffordable.** Fabs must switch to e-beam metrology.

---

## V. Limitations & the Path Forward

### Why Optical Cannot Scale Below 100nm

1. **Physics:** Diffraction limit is immutable
2. **Contrast:** Deep-UV contrast too low for reliable detection
3. **Throughput:** Multi-spectral imaging too slow for production

### The E-Beam Solution

E-beam metrology (Chapter 3) uses **electron wavelength (~0.1 nm at 10 keV acceleration voltage),** achieving ~5-10 nm resolution.

**Trade-off:** E-beam is slower (100-300 wafers/month) but accurate. Optical + E-beam hybrid approaches emerging (Chapters 2-3).

### Machine Learning Compensation

Some fabs attempt to improve optical AOI through machine learning (Chapter 4): train neural networks to infer defects from noisy optical images.

**Limited success:** ML can reduce false positives but cannot overcome diffraction limit for small defects. E-beam metrology still required.

---

## VI. Capital Allocation: The AOI → E-Beam Transition

### Market Dynamics (2024-2028)

**Optical AOI market:** Declining; mature technology
- Annual sales: $2-2.5B (shrinking 5-10%/year)
- Growth from OSAT (outsourced assembly), mature nodes only

**E-Beam metrology market:** Explosive growth
- Annual sales: $3-4B (growing 20-25%/year)
- Driven by sub-3nm capacity ramps

### Equipment Vendor Impact

**Vendors with strong optical AOI business:**
- Must transition customers to e-beam metrology
- Margins compress during transition (margin difference: 50% optical vs. 50% e-beam)
- **ROIC stable** but growth rate declining

**Vendors with early e-beam leadership:**
- Capture growing sub-3nm inspection capex
- Higher ROIC (28-35%) due to advanced technology
- **Growth rate:** 20-25% annually through 2028

---

## VII. Real-World Example: 3nm Node Inspection

**TSMC N3 (3nm node) inspection plan:**

| Layer | Optical AOI | E-Beam SEM | Purpose |
|---|---|---|---|
| Lithography (photoresist) | ✓ | ✗ | Quick check; defects >100nm |
| Etch (gate/trench) | ✗ | ✓ | SEM required; defects ~20-50nm |
| Deposition (dielectric) | ✓ (multi-spec) | ✓ (spot-check) | Both used; E-beam confirms anomalies |
| Metal (interconnect) | ✗ | ✓ | Voids, bridges <100nm; E-beam only |
| CMP (planarization) | ✓ | ✓ | Optical for throughput; E-beam for anomalies |

**Result:** N3 fabs require **8-12 e-beam tools + 6-8 optical tools** for comprehensive inspection.

Capex: $15-20M per fab just for metrology (not counting lithography, etch, other equipment).

---

## Summary

Optical inspection was the industry standard from 1990-2015. It defined how fabs approach metrology: real-time feedback, automated defect classification, statistical process control.

But **diffraction physics makes optical inspection obsolete for sub-3nm nodes.**

The transition to e-beam metrology (Chapters 3-5) is therefore **inevitable and expensive**—exactly the conditions that create equipment vendor moats and high capital allocation ROI.

---

**Next:** [Chapter 2: Defect Detection Algorithms](02-defect-detection-algorithms.md)
