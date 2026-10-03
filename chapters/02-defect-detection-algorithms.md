# Chapter 2: Defect Detection Algorithms

## From Images to Defect Lists

Optical inspection captures terabytes of images daily. A 100K wafers/month fab generates 500TB+ of raw inspection imagery. Humans cannot analyze this. Algorithms must.

This chapter reveals the statistical and machine learning approaches that turn raw images into actionable defect reports.

---

## I. Inversion: Algorithm Failures

### Failure 1: False Positive Explosion

If defect detection algorithm has 50% false positive rate, fab operators spend 90% of time chasing phantom defects.

**Consequence:** Real defects go unfixed. Yield continues to degrade.

### Failure 2: False Negative Defects

If algorithm misses real defects (false negative rate >5%), undetected defects propagate downstream. Yield collapses at final test.

### Failure 3: Slow Processing

If algorithm takes >1 second per image, a 100K wafers/month fab cannot process inspection images in real time. Feedback loops are delayed by days.

---

## II. Physics: Statistical Defect Detection

### A. Threshold-Based Detection (Legacy)

**Simple approach:** If pixel intensity > threshold, mark as defect.

```
Defect = 1 if Intensity > T else 0
```

**Problems:**
- Fixed threshold doesn't adapt to noise variations
- No feature discrimination (large spot vs. small spot treated identically)
- High false positive rate

### B. Statistical Process Control (SPC)

**Assume:** Background pixels follow Gaussian distribution N(μ, σ²)

**Threshold:** Mark pixels >3σ above mean as suspect

```
Z-score = (Intensity - μ) / σ
Defect = 1 if |Z-score| > 3 else 0
```

**Advantage:** Adapts to local intensity variations

**Disadvantage:** Still high false positives from noise clusters

### C. Morphological Filtering

**Approach:** Use image processing to remove isolated noise, keep connected components (real defects).

```
1. Threshold image at 3σ
2. Apply morphological opening (remove small noise)
3. Apply morphological closing (fill small holes)
4. Analyze connected components
```

**Connected component size filter:**
- Small spots (1-10 pixels): Likely noise → reject
- Medium spots (10-100 pixels): Possible defect → flag
- Large spots (>100 pixels): Likely defect → report

**Effectiveness:** ~70% false positive reduction

---

## III. Machine Learning: CNNs for Defect Classification

### A. Convolutional Neural Networks (CNNs)

**Architecture:** Image → Conv layer → ReLU → Pooling → Fully connected → Softmax → Defect class

**Input:** 32×32 pixel image patch
**Output:** Probability distribution over defect classes (void, bridge, particles, background)

### B. Training Data

Equipment vendors accumulate massive defect datasets:
- 1000+ fabs × 10+ years of inspection = **billions of labeled defect images**
- Real vs. false positive examples
- Multiple defect types (voids, bridges, particles, resist residue)

**Data quality:** Equipment vendors with largest datasets have best models (winner-take-most).

### C. Model Performance

**Precision:** Of detected defects, what fraction are real?
- Target: >95% precision (false positive rate <5%)

**Recall:** Of real defects, what fraction are detected?
- Target: >90% recall (false negative rate <10%)

**Speed:** Inference time per image
- Target: <0.5 seconds per image (real-time processing)

**Real-world CNN performance (2024):**
- Precision: 92-97% (equipment vendor dependent)
- Recall: 88-94%
- Speed: 0.1-0.3 seconds per image

---

## IV. Practice: Real-Time Defect Processing

### Image Processing Pipeline

```
Raw image (8 megapixels, 50 MB)
    ↓
Downsampling (2 megapixels, 12 MB)
    ↓
Morphological preprocessing (remove noise)
    ↓
Patch extraction (32×32 patches, 500K patches)
    ↓
CNN inference on each patch (0.1s per patch)
    ↓
Defect probability map
    ↓
Connected component analysis
    ↓
Defect report (500-5000 defects per wafer)
    ↓
Database storage + fab notification
```

**Total processing time per wafer:** 10-20 minutes (acceptable for production)

### False Positive Reduction Techniques

1. **Ensemble methods:** Run multiple CNN models, vote on defects → reduces false positives 30-50%

2. **Context-aware detection:** Use adjacent images to confirm defect (isolated noise appears in one image; real defects appear in multiple layers)

3. **Semantic segmentation:** Don't just classify presence/absence; segment defect boundaries → better feature extraction

---

## V. Economics: Why Detection Matters

### Cost of False Positives

**Scenario:** 1000-wafer batch, 200 wafers flagged for investigation

Average fab spends 4 hours per wafer investigating flagged wafers = 800 hours = $50K+ in engineer time

If 50% of flags are false positives = $25K wasted investigating phantoms

Over 50K wafers/month: $625K/month waste from false positives

**Solution:** Improve CNN precision from 92% to 96% → save $200K/month

### Cost of False Negatives

**Scenario:** Real defect goes undetected

Defect propagates to final test → chip fails → warranty replacement = $200-500 loss per chip

If 1% of real defects missed, and fab produces 1M chips/month with 0.5% defect rate (5000 defective chips), missing 1% = 50 undetected defects × 100 chips per defect = 5000 chips that should have been caught → $1M+ loss

**Solution:** Improve CNN recall from 88% to 93% → save $500K+/month

---

## VI. Real-World Algorithm Performance

### Optical vs. E-Beam Defect Detection

| Metric | Optical AOI (Chapter 1) | E-Beam SEM (Chapter 3) |
|---|---|---|
| Precision | 92-94% | 97-99% |
| Recall | 85-88% | 93-96% |
| Speed | 0.1-0.3s/image | 5-10s/image |
| Throughput | 1000+ wafers/month | 100-300 wafers/month |

**Trade-off:** Optical is fast but noisy; E-beam is slow but accurate.

Fabs use **hybrid approach:** Optical for quick screening, E-beam for anomaly confirmation.

---

## Summary

Defect detection algorithms are the bottleneck between raw inspection data and actionable yield insights. Improvements in CNN precision/recall directly translate to $100K-$1M+ monthly savings for fabs.

Equipment vendors with superior algorithms (trained on large defect datasets) command premium pricing and customer lock-in.

---

**Next:** [Chapter 3: E-Beam Metrology](03-e-beam-metrology.md)
