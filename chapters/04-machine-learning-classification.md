# Chapter 4: Machine Learning Classification

## The Data Moat

Every defect image collected becomes training data. Equipment vendors with 5,000+ installed tools globally have accumulated billions of labeled defect images.

This is the **ultimate competitive moat:** convolutional neural networks trained on billions of real manufacturing defects from 1,000+ fabs can detect anomalies with 97%+ accuracy.

Competitors cannot acquire this dataset. It is proprietary, accumulated over 10-15 years, and legally protected.

---

## I. Model Architecture

**CNN for defect classification:**

```
Input: 64×64 pixel E-beam image
  ↓
Conv1: 32 filters, 3×3 kernel, ReLU
  ↓
Pool1: 2×2 max pooling
  ↓
Conv2: 64 filters, 3×3 kernel, ReLU
  ↓
Pool2: 2×2 max pooling
  ↓
Flatten
  ↓
Dense1: 128 units, ReLU
  ↓
Dense2: 64 units, ReLU
  ↓
Output: Softmax (5 classes: void, bridge, particle, resist, background)
```

**Parameters:** ~200K trainable parameters

**Training:** 1 billion labeled images → 50 epochs → convergence in 2-4 weeks on GPU cluster

---

## II. Performance Metrics

**Precision by defect class:**

| Defect Type | Precision | Recall | F1 Score |
|---|---|---|---|
| Void | 96% | 92% | 0.94 |
| Bridge | 94% | 89% | 0.91 |
| Particle | 97% | 94% | 0.95 |
| Resist residue | 88% | 85% | 0.86 |
| Background (true negative) | 99% | 98% | 0.98 |

---

## III. Model Drift & Retraining

**Problem:** Model trained on 2022 data performs poorly on 2026 data (new materials, new process recipes, equipment drift).

**Solution:** Continuous retraining
- Collect new labeled defects daily
- Retrain model weekly
- A/B test new model on live data before deployment

**Cost:** $500K-$1M/year per fab for model maintenance

---

## IV. Competitive Advantage

Equipment vendors with largest defect datasets → best ML models → highest precision/recall → customer preference → larger installed base → larger future dataset → **winner-take-most dynamics**

This is why industry consolidation is inevitable. By 2030, 1-2 vendors will dominate metrology through ML moat alone.

---

**Next:** [Chapter 5: Process Control & Feedback](05-process-control-feedback.md)
