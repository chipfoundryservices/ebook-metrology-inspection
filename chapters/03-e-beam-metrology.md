# Chapter 3: E-Beam Metrology — Precision at the Nanoscale

## Electron Wavelength: The Solution to Diffraction

Optical light has wavelength 193-365 nm. Electrons accelerated through 10 kV potential have de Broglie wavelength ~0.12 nm.

**Electron wavelength is 2,000x smaller than light.** This enables 5-10 nm resolution—enough to detect all manufacturing defects at 3nm nodes.

---

## I. Inversion: E-Beam Challenges

### Failure 1: Charging Effects

Electrons accumulate on insulating surfaces (dielectrics), creating positive charge buildup. Subsequent electrons are repelled, distorting image.

**Consequence:** Image contrast degrades; defects become invisible.

**Solution:** Charge neutralization (electron flood gun) or conductive coating

### Failure 2: Beam Damage

High-energy electron beam can ionize materials, creating defects that weren't there before. Measurement becomes destructive.

**Consequence:** E-beam inspection damages wafer; cannot use for production.

**Solution:** Ultra-low beam voltage (1-3 keV instead of 10+ keV) and current limiting

### Failure 3: Slow Throughput

E-beam scans sequentially; cannot parallelize like optical (which images entire wafer at once).

**Consequence:** 100-300 wafers/month throughput (vs. 1000+ for optical)

---

## II. Physics: Electron-Matter Interactions

### A. Elastic Scattering (Image Contrast)

Electrons scatter off atomic nuclei, creating backscattered electrons (BSE). BSE yield depends on atomic number Z.

```
Contrast = (BSE_defect - BSE_background) / BSE_background
```

**Example:** Void has no material (zero BSE); copper via has high BSE → high contrast

### B. Voltage Contrast (Measurement)

Subsurface potential differences create voltage contrast without material contrast.

**Use case:** Detecting voids in metal layers (hidden beneath dielectric)

---

## III. Practice: Scanning Electron Microscope (SEM) Design

**Key components:**
- Electron gun (thermionic or field emission)
- Accelerating column (1-10 kV)
- Scanning coils (deflect beam across surface)
- Detector (backscattered electrons, secondary electrons)
- Stage (XYZ movement, temperature control)

**Specifications:**
- Resolution: 5-10 nm
- Throughput: 100-300 wafers/month
- Cost: $2-4M per tool
- Service cost: $200-300K/year

---

## IV. Economics: Why E-Beam Is Expensive

**Equipment vendor revenues from E-Beam metrology:**
- Annual sales: $3-4B (growing 20-25% annually)
- Gross margin: 50-55%
- Service margin: 70-75%
- ROIC: 28-35%

E-Beam is slower than optical but commands higher prices (superior technology) and longer customer lock-in (difficult recipes to replicate).

---

**Next:** [Chapter 4: Machine Learning Classification](04-machine-learning-classification.md)
