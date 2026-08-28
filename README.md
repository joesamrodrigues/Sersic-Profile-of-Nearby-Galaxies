# Photometric Analysis and Morphological Classification of Nearby Galaxies

**MSc Astrophysics — Cardiff University, 2023/2024**  
Supervised by Dr Paul Roche  
School of Physics and Astronomy  
*Project planned in Semester 1, completed in Semester 2*

---

## Overview

This project performs photometric analysis on telescope images of nearby galaxies and uses the Sérsic model to classify their morphological type. Single and double Sérsic profiles are fitted to the surface brightness profiles of three galaxies — NGC 3982 (spiral), NGC 2865 (elliptical), and NGC 7773 (barred spiral) — and the resulting Sérsic indices are compared against existing classifications in the literature.

The full research report is available in this repository.

---

## Galaxies Analysed

| Galaxy | Type | Redshift | Sérsic Index (Single Fit) | Classification |
|--------|------|----------|--------------------------|----------------|
| NGC 3982 | Intermediate spiral | z = 0.003699 | 0.859 | Spiral (n < 2.5) ✓ |
| NGC 2865 | Elliptical | z = 0.008683 | 2.216 | Borderline elliptical |
| NGC 7773 | Barred spiral | z = 0.028300 | 1.714 | Spiral (n < 2.5) ✓ |

Galaxies with n > 2.5 are classified as early-type (elliptical); n < 2.5 as late-type (spiral). Results are broadly consistent with existing classifications, with discrepancies attributed to foreground star contamination.

---

## Methodology

**Data Acquisition**
- Galaxy images captured using the MuSCAT3 instrument — a four-channel simultaneous imager on the 2-metre Faulkes Telescope North at Haleakalā Observatory, Maui, Hawaii
- Observations taken between 18–31 December 2023 with 60-second exposures
- Images stored in FITS format and read using Astropy

**Photometric Analysis**
- Galaxy centre identified as the pixel with maximum flux value
- Concentric circular apertures drawn using Photutils `CircularAperture`
- Flux measured in each aperture using `ApertureStats`
- Flux density calculated between consecutive apertures: Flux density(i+1, i) = flux / π(r²ᵢ₊₁ − r²ᵢ)
- Radii converted from pixels to arcseconds using MuSCAT3 pixel scale (0.27 arcsec/pixel)
- Surface brightness profile plotted as flux density vs radius (log-log scale)

**Sérsic Model Fitting**
- Single-Sérsic model fitted to full surface brightness profile using `scipy.optimize.curve_fit` with `Astropy Sersic1D`
- Double-Sérsic model fitted separately to bulge and disk regions by selecting data points above and below a radius threshold, then combining both `Sersic1D` functions simultaneously
- Sérsic indices compared against literature values

**Edge-on Galaxies**
- NGC 4565 was analysed using elliptical apertures but could not produce an accurate light curve due to inclination effects
- NGC 891 and NGC 4013 were not analysed for the same reason

---

## Key Results

- **NGC 3982** — Sérsic index n = 0.859 (single fit), consistent with spiral classification. Bulge index nᵦ = 0.791 indicates a pseudobulge, characteristic of spiral galaxies. Compared to literature value nᵦ = 1.95 ± 0.19 — same morphological classification despite numerical difference.
- **NGC 2865** — Sérsic index n = 2.216, borderline elliptical. Foreground star contamination affected the fit. Bulge index suggests pseudobulge, which is atypical for elliptical galaxies.
- **NGC 7773** — Sérsic index n = 1.714, consistent with spiral/barred spiral classification. Double-Sérsic fit heavily degraded by a nearby foreground object.

---

## Tools and Software

| Tool | Purpose |
|------|---------|
| Python | Analysis and visualisation |
| Astropy | FITS file reading, Sérsic1D model, aperture tools |
| Photutils | Circular aperture photometry, flux measurement |
| SciPy | `curve_fit` optimisation for Sérsic fitting |
| NumPy / Matplotlib | Numerical computation and plotting |
| Google Colab | Development environment |

---

## Repository Contents

| File | Description |
|------|-------------|
| `Micro_Project.ipynb` | Full analysis notebook — photometry, Sérsic fitting, plots |
| `Rodrigues_PXT992_paper_report.pdf` | Research report submitted for the module |
| `research_diary` | Research diary kept throughout the project |
| `FITS` | Raw FITS telescope images for NGC 3982, NGC 2865, NGC 7773 |

---

## Development Notes

Code in this project came from several sources:

- **Aperture photometry and plotting** — written independently with reference to online resources, documentation, and YouTube tutorials
- **Sérsic fitting framework** — provided by a PhD student supporting the project; the original code was from a previous research group, as acknowledged in the research report ("the python code lines accessible which were available from the previous research group" — Acknowledgements)
- The analysis, interpretation, parameter tuning, and written commentary were completed independently

---

## Data Access

Galaxy images were obtained using the Faulkes Telescope Network. Similar data for these galaxies is publicly available via:
- [NASA/IPAC Extragalactic Database (NED)](https://ned.ipac.caltech.edu/)
- [Las Cumbres Observatory (LCO) archive](https://archive.lco.global/)

---

## Acknowledgements

Dr Paul Roche (supervision and code guidance), Dipanjan Mitra (research guidance), Dr Andreas Papageorgiou (Python support).

---

## Key References

- Fisher & Drory (2010) — Bulges of nearby galaxies with Spitzer, *The Astrophysical Journal*
- Graham & Driver (2005) — Sérsic R^{1/n} quantities reference
- Vulcani et al. (2014) — Galaxy And Mass Assembly (GAMA), MegaMorph
- NASA/IPAC Extragalactic Database — redshift values
