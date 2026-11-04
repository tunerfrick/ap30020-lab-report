---
name: ap30020-lab-report
description: Process raw AP30020 semiconductor lab data into fitted plots and a written analysis section. Use for experiments E1-E9 when a log sheet or CSV of measurements is provided.
---

# AP30020 lab report

Turn raw measurements from one experiment into (a) the figures and (b) the
analysis prose that goes under them. Follow the conventions below exactly;
where a judgement call is flagged, stop and ask rather than deciding.

## Inputs

A table of measurements for one experiment, as CSV or pasted from the log
sheet. Column meanings come from the experiment number (E1 = T and V_diode,
E3 = I and V per diode, E4 = R/I/V plus d/I_L/V_max, E6 = I_B/I_C/V_ce,
E7 = I_D/V_DS). If the experiment is unclear from the columns, ask.

## Fitting

- Linear least-squares. Report uncertainties as the **standard errors of the
  fit parameters**, never as a guessed instrument precision.
- Write fitted relations in the form
  `V = (-2.375 +/- 0.042)e-3 T + (1.213 +/- 0.013)`.
- Always quote R^2, and state the number of points and the range they cover:
  "Linear least-squares fit (11 points, 295-345 K)".
- Results to 3 significant figures; uncertainties to 1-2.
- State kT/e = 0.0257 V explicitly wherever it enters a calculation.
- When a model is linear in its unknowns (e.g. V = eta(kT/e)ln(I/I0) + I*Rs),
  fit all unknowns simultaneously by least squares rather than fitting a
  slope and then correcting it.

## The constant-ratio check

**Run this before accepting any fitted parameter.** Compute the obvious
ratios in the data and look for one that should vary with the physics but
comes out constant, or one that should be constant but drifts.

A ratio that holds fixed across every point - especially across two
different devices - is a circuit element, not the device under test. Work
out what it corresponds to (series resistance in the leads or ammeter, a
meter still in circuit when it should have been disconnected) and report the
parameter both before and after removing it.

Precedents: (V - V_on)/I came to ~470 ohm at every point for both the Si
diode and the LED in E3, which is lead/ammeter resistance and inflated the
apparent eta to 63. V_max/I_L was 5.5 +/- 0.1 ohm at all seven distances in
E4, which is Ohm's law across the 5.7 ohm ammeter that was still shorting
the cell, so the voltmeter was reading the ammeter's drop and not V_max.

If the check fires, say so in the Method note and plot both panels (below).

## Plots

- Axis labels as `Quantity / unit`, symbol italic: `V_diode / V`, `I_C / mA`,
  `1/d^2 / m^-2`.
- Title as "X versus Y", e.g. "Si diode: V_diode versus T".
- Measured points: solid black circles. Fit: line, with the fitted equation
  and R^2 in the legend.
- Extrapolations beyond the data: dashed, with the intercept annotated on the
  axis.
- Excluded points: keep them on the plot with a distinct marker (x) and label
  them in the legend. Never silently drop a point.
- Two panels side by side when a correction is being demonstrated:
  (a) raw, (b) after removing the correction.
- Grid on. Shade a region only when the area means something (the
  maximum-power rectangle in E4), and give it its value in the legend.

## Written analysis

- Open with a bolded `Method.` paragraph whenever the processing is not
  obvious from the plot. Terse and dense; no restating of the manual.
- Compare against the tabulated or theoretical value with an explicit
  percentage difference.
- List systematic errors inline and numbered: (i) ... (ii) ... (iii) ...
- Close by stating how the measurement should have been made instead.
- Match the voice of the existing reports: first person plural for what was
  done ("our data support this"), plain declarative sentences, no hedging
  filler.

## Stop and ask

Flag these; do not decide them.

- **Outliers.** A candidate is a point whose residual is roughly an order of
  magnitude above the others. Check whether a single misread digit would put
  it on the fit (the E3 6800 uA point read 3.430 V where 3.930 V fits) and
  report that, then ask before excluding.
- **Which region is "active"** or linear, when the boundary is not forced by
  the data.
- **Ranking systematic errors** by plausibility. Produce the candidate list;
  the ordering is the author's.
- Any case where the constant-ratio check fires but no plausible circuit
  element accounts for it.

## Output

Figures as PNG, named `E<n>_<quantity>.png`. The analysis as markdown ready
to paste under the figure, with the fitted equation displayed on its own
line. Report what was fitted, over what range, and anything flagged above.
