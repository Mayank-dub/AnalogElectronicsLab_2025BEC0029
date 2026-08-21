## RC Low-Pass Filter — AC Analysis (Cadence Virtuoso, Spectre)

### Circuit
- R = 1 kΩ
- Vin = sine source, AC magnitude = 1 V
- C swept across three values: 1 µF, 10 µF, 20 µF

### Method
AC analysis (log sweep, 1 Hz – 1 MHz) run in ADE L for each capacitor value.
Gain plotted as dB20(Vout) vs log(frequency). -3dB frequency extracted using
a marker on the dB-vs-frequency curve (Y = -3 dB crossing).

### Results

| C (µF) | Theoretical f₋₃dB = 1/(2πRC) | Simulated f₋₃dB | % Error |
|--------|-------------------------------|------------------|---------|
| 1      | 159.15 Hz                     | 159 Hz           | ~0.10%  |
| 10     | 15.92 Hz                      | 15.88 Hz         | ~0.25%  |
| 20     | 7.96 Hz                       | 7.939 Hz         | ~0.26%  |

### Observations
- Simulated bandwidth closely matches theoretical predictions across all
  three cases (sub-0.3% error), as expected for ideal lumped R and C with
  no parasitics.
- Bandwidth decreases as C increases — consistent with f₋₃dB ∝ 1/C.
  Increasing C by 10× (1 µF → 10 µF) drops the cutoff by ~10×; increasing
  C by 2× (10 µF → 20 µF) drops it by ~2×, confirming the inverse
  proportionality.
- Physical explanation: capacitor impedance Z_C = 1/(jωC) decreases faster
  with frequency as C grows, so in the R–C voltage divider, the output
  starts getting shorted to ground at progressively lower frequencies. A
  larger capacitor therefore narrows the passband — it filters out lower
  frequencies too, at the cost of bandwidth.

### Conclusion
Capacitance and bandwidth are inversely related in an RC low-pass filter.
For a fixed R, increasing C is a direct trade-off: better attenuation of
high frequencies, but a narrower passband.
