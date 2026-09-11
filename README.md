# CPET IC Dynamics Calculator

A small browser-based calculator for serial inspiratory capacity during CPET. It derives inspiratory capacity and inspiratory reserve volume from paired tidal volume and VT/IC values reported in the exercise flow-volume-loop table.

## Important: use the ExFVL table

Use paired values from the same row of the table labeled `ExFVL`:

- `Vt`
- `Vt/IC`

Enter the resting row and each available exercise row.

Do **not** use the separate `AT / VO2 Max` summary table. In the reviewed Mayo CPET reports, those values are averaged at physiologic landmarks and do not necessarily correspond to the discrete IC maneuvers shown in the ExFVL table. Mixing the two sources can produce internally inconsistent calculated IC values.

## Inputs

- Rest VT and VT/IC (required)
- Exercise 1 VT and VT/IC (required); Exercise 2 to 4 optional
- Workload in watts for each exercise maneuver, optional; when entered, the chart and report sentence state when the change occurred

## Calculations

```text
IC = VT / (VT/IC)
IRV = IC - VT
```

Because the source report rounds VT/IC to a whole percentage (±0.5) and VT to 0.01 L (±0.005), each calculated IC has a plausible range:

```text
IC range = (VT ± 0.005) / (VT/IC ± 0.5%)
```

The range for a change from rest combines the resting and exercise ranges conservatively. The resting maneuver dominates the uncertainty because its VT/IC is smallest.

The calculator reports:

- Calculated IC and IRV for each maneuver, with plausible ranges
- Maximum IC decrease from rest, in liters and percent, with a range
- Maximum exercise VT/IC
- Minimum exercise IRV, with a range
- Dynamic-hyperinflation category
- Inspiratory mechanical-constraint category
- A copy-ready report sentence

## Operational interpretation used by the app

Dynamic hyperinflation (thresholds: IC decrease of at least 0.15 L and at least 10% from rest):

- **Clear:** the entire plausible range of the IC fall meets both thresholds, so the finding is robust to rounding
- **Borderline:** the point estimate meets at least one threshold but the range does not clear both, or the point estimate meets neither but the range cannot exclude both
- **Not clear:** neither threshold is met and the range does not reach both

Published studies have used an IC decrease of 0.15 L, 10%, or either criterion. Because this app reconstructs IC from rounded values rather than reading a directly measured IC, it requires the finding to survive the rounding uncertainty before calling it clear.

Inspiratory mechanical constraint:

- **Marked:** IRV at most 0.5 L
- **Approaching:** VT/IC at least 60% or IRV at most 1.0 L
- **Not clear:** neither condition is met

VT/IC alone does not trigger "marked" because IRV = IC x (1 - VT/IC): a patient with a large IC can reach VT/IC of 70% with more than 1 L of IRV remaining.

These are practical descriptors, not universal diagnostic cutoffs. Review the flow-volume loops, maneuver quality, breathing pattern, spirometry, and the complete CPET. A fall in calculated IC assumes adequate IC maneuvers; a submaximal inspiratory effort at high ventilation mimics hyperinflation.

## Compatibility

The calculator is useful when the CPET report includes serial exercise flow-volume loops and an ExFVL table containing paired VT and VT/IC values.

It cannot calculate serial IC from reports that provide tidal volume alone. Older treadmill or cardiology CPET reports may not include VT/IC or exercise IC maneuvers.

## Built-in example

The `Load example` button enters:

```text
Rest:       VT 1.83 L, VT/IC 53%
Exercise 1: VT 1.98 L, VT/IC 66%, 60 W
Exercise 2: VT 1.93 L, VT/IC 64%, 120 W
```

Expected result:

```text
Rest IC: about 3.45 L (range 3.41 to 3.50)
Lowest exercise IC: about 3.00 L
Maximum IC decrease: about 0.45 L, 13% (range 0.38 to 0.53 L)
Dynamic hyperinflation: clear (robust to rounding)
Inspiratory constraint: approaching (minimum IRV 1.02 L)
```

## Files

```text
index.html
README.md
```

The app is contained entirely in `index.html`. It has no server, database, analytics, or external JavaScript dependencies. All calculations occur in the browser.

## Publish with GitHub Pages

Create a public GitHub repository, upload `index.html` and `README.md` to the repository root, and commit them to the `main` branch.

Then open:

```text
Settings > Pages
```

Choose:

```text
Source: Deploy from a branch
Branch: main
Folder: /(root)
```

Save the setting. The site address will normally be:

```text
https://YOUR-GITHUB-USERNAME.github.io/cpet-ic-dynamics/
```

## Updating the site later

Upload a replacement `index.html` to the same repository root and commit it to `main`. GitHub Pages will redeploy the site automatically.

## Version

1.2 (2026-09-11). Version and date are shown on the page.

## References

- O'Donnell DE, Elbehairy AF, Webb KA, Neder JA. The Link between Reduced Inspiratory Capacity and Exercise Intolerance in Chronic Obstructive Pulmonary Disease. *Ann Am Thorac Soc*. 2017;14(Suppl 1):S30-S39. doi:10.1513/AnnalsATS.201610-834FR.
- Collins SE, et al. Smaller Airways or Bigger Lungs? Dysanapsis Etiotypes and Obstructive Pulmonary Physiology at Rest and During Exercise. *Am J Respir Crit Care Med*. 2025;211:1519-1522. doi:10.1164/rccm.202501-0205RL. This study defined dynamic hyperinflation as a rest-to-peak IC decrease greater than 0.15 L and used VT/IC at least 70% in a sensitivity analysis for critical inspiratory constraint.
- Huber dos Santos A, et al. Metronome-paced tachypnea test cutoff value for detecting dynamic hyperinflation in COPD: A diagnostic accuracy study. *Respir Med*. 2026;260:108924. doi:10.1016/j.rmed.2026.108924. This study defined CPET dynamic hyperinflation as an IC reduction of at least 10% and/or at least 0.15 L.
