# Mathematical Derivations

## 1. Optical Resolution (Rayleigh Criterion)

**Derivation:**

The minimum resolvable distance between two point sources is limited by diffraction:

```
d = λ / (2 × NA)
```

**Application (Chapter 1):**
- λ = 193 nm (deep-UV)
- NA = 0.9 (high-quality lens)
- d = 193 / (2 × 0.9) = 107 nm

**Consequence:** Cannot resolve defects <100 nm with optical inspection.

---

## 2. De Broglie Wavelength of Electrons

**Derivation:**

From quantum mechanics, particles have wavelength:

```
λ = h / p = h / √(2mE)
```

Where:
- h = Planck's constant (6.626 × 10⁻³⁴ J·s)
- p = momentum
- m = electron mass (9.109 × 10⁻³¹ kg)
- E = kinetic energy

**Application (Chapter 3):**
- E = 10 keV = 1.6 × 10⁻¹⁵ J
- λ = 6.626 × 10⁻³⁴ / √(2 × 9.109 × 10⁻³¹ × 1.6 × 10⁻¹⁵)
- λ ≈ 0.12 nm

**Consequence:** E-beam wavelength is 2,000x smaller than light → 2,000x better resolution.

---

## 3. SPC Control Limits

**Derivation:**

Assuming normal distribution with mean μ and standard deviation σ:

```
UCL = μ + 3σ
LCL = μ - 3σ
```

**Interpretation:** 99.73% of measurements fall within [LCL, UCL]

**Application (Chapter 5):**
- If measurement > UCL, probability of random variation is <0.135%
- Process is out of control; investigate and adjust

---

## 4. CNN Accuracy Metrics

**Precision:**
```
Precision = TP / (TP + FP)
```

Where TP = true positives, FP = false positives

**Recall:**
```
Recall = TP / (TP + FN)
```

Where FN = false negatives

**F1 Score:**
```
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

---

## 5. Yield Learning Curve (S-Curve Model)

**Empirical model:**

```
Yield(t) = Y_max / (1 + exp(-k(t - t_0)))
```

Where:
- Y_max = maximum achievable yield (~95%)
- k = learning rate
- t_0 = inflection point (typically 6-12 months into ramp)

**Application (Chapter 7):**
- fab with superior metrology: k = 0.5 (steep learning curve, 95% in 18 months)
- fab with inferior metrology: k = 0.3 (shallow curve, 95% in 24+ months)

---

## 6. Equipment ROI

**Simple payback calculation:**

```
Payback period = Equipment capex / Annual yield improvement profit
```

**Application (Chapter 7):**
- Equipment capex: $15M
- Annual yield improvement: $30-50M
- Payback period: 15M / 40M = **3.75 months**

---

**End of Mathematical Appendix**
