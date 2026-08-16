# CPET IC Dynamics Calculator

A small browser-based calculator for serial inspiratory capacity during CPET. It derives inspiratory capacity and inspiratory reserve volume from paired tidal volume and VT/IC values reported in the exercise flow-volume-loop table.

## Important: use the ExFVL table

Use paired values from the same row of the table labeled `ExFVL`:

- `Vt`
- `Vt/IC`

Enter the resting row and each available exercise row.

Do **not** use the separate `AT / VO2 Max` summary table. In the reviewed Mayo CPET reports, those values are averaged at physiologic landmarks and do not necessarily correspond to the discrete IC maneuvers shown in the ExFVL table. Mixing the two sources can produce internally inconsistent calculated IC values.

## Inputs

- Rest VT and VT/IC
- Exercise 1 VT and VT/IC
- Exercise 2 VT and VT/IC, optional
- Exercise 3 VT and VT/IC, optional

At least one exercise maneuver is required.

## Calculations

```text
IC = VT / (VT/IC)
IRV = IC - VT
```

The calculator reports:

- Calculated IC and IRV for each maneuver
- Maximum IC decrease from rest, in liters and percent
- Maximum exercise VT/IC
- Minimum exercise IRV
- Dynamic-hyperinflation category
- Inspiratory mechanical-constraint category
- A copy-ready report sentence

Because the source report rounds VT/IC to a whole percentage, calculated IC and IRV are approximate.

## Operational interpretation used by the app

Dynamic hyperinflation:

- **Clear:** IC decreases by at least 0.15 L **and** at least 10% from rest
- **Borderline:** only one of those thresholds is met
- **Not clear:** neither threshold is met

Published studies have used an IC decrease of 0.15 L, 10%, or either criterion. Because this app reconstructs IC from whole-number VT/IC values rather than reading a directly measured IC, it deliberately uses the more conservative three-level scheme above.

Inspiratory mechanical constraint:

- **Marked:** VT/IC at least 70% or IRV at most 0.5 L
- **Approaching:** VT/IC 60% to 69% or IRV 0.51 to 1.0 L
- **Not clear:** neither condition is met

These are practical descriptors, not universal diagnostic cutoffs. Review the flow-volume loops, maneuver quality, breathing pattern, spirometry, and the complete CPET.

## Compatibility

The calculator is useful when the CPET report includes serial exercise flow-volume loops and an ExFVL table containing paired VT and VT/IC values.

It cannot calculate serial IC from reports that provide tidal volume alone. Older treadmill or cardiology CPET reports may not include VT/IC or exercise IC maneuvers.

## Built-in example

The `Load example` button enters:

```text
Rest:       VT 1.83 L, VT/IC 53%
Exercise 1: VT 1.98 L, VT/IC 66%
Exercise 2: VT 1.93 L, VT/IC 64%
```

Expected result:

```text
Rest IC: about 3.45 L
Lowest exercise IC: about 3.00 L
Maximum IC decrease: about 0.45 L, 13%
Dynamic hyperinflation: clear
Inspiratory constraint: approaching
```

## Files

```text
index.html
README.md
```

The app is contained entirely in `index.html`. It has no server, database, analytics, or external JavaScript dependencies. All calculations occur in the browser.

## Publish with GitHub Pages

Suggested repository name:

```text
cpet-ic-dynamics
```

Suggested description:

```text
CPET serial inspiratory capacity and dynamic hyperinflation calculator
```

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

## References

- O'Donnell DE, Elbehairy AF, Webb KA, Neder JA. The Link between Reduced Inspiratory Capacity and Exercise Intolerance in Chronic Obstructive Pulmonary Disease. *Ann Am Thorac Soc*. 2017;14(Suppl 1):S30-S39. doi:10.1513/AnnalsATS.201610-834FR.
- Collins SE, et al. Smaller Airways or Bigger Lungs? Dysanapsis Etiotypes and Obstructive Pulmonary Physiology at Rest and During Exercise. *Am J Respir Crit Care Med*. 2025;211:1519-1522. doi:10.1164/rccm.202501-0205RL. This study defined dynamic hyperinflation as a rest-to-peak IC decrease greater than 0.15 L and used VT/IC at least 70% in a sensitivity analysis for critical inspiratory constraint.
- Huber dos Santos A, et al. Metronome-paced tachypnea test cutoff value for detecting dynamic hyperinflation in COPD: A diagnostic accuracy study. *Respir Med*. 2026;260:108924. doi:10.1016/j.rmed.2026.108924. This study defined CPET dynamic hyperinflation as an IC reduction of at least 10% and/or at least 0.15 L.
