# Chapter 5: Process Control & Feedback Loops

## SPC to APC: From Monitoring to Controlling

**SPC (Statistical Process Control):** Monitor process; alert when out of spec

**APC (Advanced Process Control):** Automatically adjust process parameters in real time based on metrology feedback

---

## I. SPC Framework

**Collect:** Wafer measurements (thickness, defect count, etc.)

**Plot:** Control chart with UCL (upper control limit) and LCL (lower control limit)

**Alert:** If measurement > UCL or < LCL, process is out of control; investigate and correct

**Typical limits:** ±3σ (99.7% of measurements should fall within)

---

## II. APC: Closed-Loop Optimization

**Real-time feedback loop:**

```
Wafer N measurement
    ↓
Compare to setpoint
    ↓
Calculate adjustment (PID control)
    ↓
Send command to upstream tool (CVD, etch, lithography)
    ↓
Wafer N+1 processed with adjusted parameters
    ↓
Measure wafer N+1
    ↓
Repeat
```

**Example:** Copper thickness trending 2% high

→ Equipment sends "reduce deposition voltage by 0.5V"

→ Next wafer thickness within spec

---

## III. Economics: APC ROI

**Benefit:** 1% yield improvement = $30-50M annually for 100K wafers/month fab

**Cost:** APC software + integration = $2-5M (one-time) + $500K/year (maintenance)

**Payback period:** 1-3 months

This is why fabs aggressively adopt APC despite high integration complexity.

---

**Next:** [Chapter 6: Competitive Moats — Equipment Dominance](06-kla-competitive-moats.md)
