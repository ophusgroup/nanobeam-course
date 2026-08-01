---
title: Orientation mapping (ACOM)
---

# Automated crystal orientation and phase mapping

**11:15 – 12:00 · Colin Ophus · Colab demo**

```{image} ../assets/cover-orientation.jpg
:alt: Schematic of automated crystal orientation mapping — diffraction patterns from a polycrystalline film are matched against a library of simulated patterns over all orientations
:width: 100%
```

Most functional and structural materials are polycrystalline, and their properties depend on grain size, texture, grain boundary character, and phase distribution. Automated crystal orientation mapping (ACOM) in 4D-STEM measures all of these: at every probe position, the recorded diffraction pattern is matched against a library of patterns simulated over all possible crystal orientations, and the best match assigns a local orientation — like electron backscatter diffraction (EBSD) in the SEM, but in transmission, with nanometer resolution, and on the same datasets used for every other analysis in this course.

## How it works

1. **Reference structures.** Load the candidate crystal structures (e.g., from CIF files) and compute their structure factors up to the maximum scattering vector recorded on the detector.
2. **Orientation plan.** Simulate diffraction patterns over a grid of orientations covering the symmetry-reduced zone axis range — a lookup table of expected Bragg peak positions and intensities. Grid spacings of a few degrees, with local refinement, balance accuracy against speed.
3. **Bragg peak detection.** As for strain mapping, detect the diffraction peaks at every probe position (the same calibrated Bragg vectors feed both analyses).
4. **Correlation matching.** For each probe position, score the measured peaks against the orientation library and keep the best match(es) — returning multiple matches with a minimum angular separation handles overlapping grains along the beam direction.
5. **Orientation and phase maps.** The result is an orientation map (typically displayed with inverse-pole-figure coloring for in-plane and out-of-plane directions), plus per-position correlation scores. Running plans for multiple candidate phases and comparing their correlation scores produces a **phase map** — and quantitative phase-fraction estimates.

## Precession and pattern quality

Zone-axis nanobeam patterns are strongly dynamical: intensities oscillate with thickness and small mistilts, which degrades matching against kinematical templates. **Precession electron diffraction (PED)** — rocking the beam on a cone (typically ~0.3–1°) while descanning below the sample — integrates through the rocking curve and produces more kinematical-like, more complete patterns. Precession substantially improves both orientation reliability and phase discrimination, and the tutorial dataset for this block is a precession 4D-STEM measurement of a two-phase (α + β) titanium alloy.

## Practical notes

- Pattern matching is only as good as the calibration: the reciprocal pixel size can be refined by fitting the measured Bragg peak radial distribution against the structure factors of a known phase in the sample.
- Correlation score maps are worth inspecting on their own — low scores flag overlapping grains, unindexed phases, or regions where the library doesn't contain the right structure.
- Template matching of the *full patterns* (as in pyxem) and sparse peak matching (as in py4DSTEM's ACOM) are complementary approaches; both are open source, so you can try each on your data.

## Tutorial

:::{important}
🚧 **Google Colab notebook link coming soon.** The tutorial notebooks are being updated for the course and will be linked here.

In the meantime, see the [py4DSTEM tutorials repository](https://github.com/py4dstem/py4DSTEM_tutorials).
:::

## References

- C. Ophus et al., "Automated Crystal Orientation Mapping in py4DSTEM using Sparse Correlation Matching," *Microscopy and Microanalysis* **28**, 390–403 (2022). [doi:10.1017/S1431927622000101](https://doi.org/10.1017/S1431927622000101)
- E. F. Rauch and M. Véron, "Automated crystal orientation and phase mapping in TEM," *Materials Characterization* **98**, 1–9 (2014). [doi:10.1016/j.matchar.2014.08.010](https://doi.org/10.1016/j.matchar.2014.08.010)
- N. Cautaerts et al., "Free, flexible and fast: Orientation mapping using the multi-core and GPU-accelerated template matching capabilities in the Python-based open source 4D-STEM analysis toolbox Pyxem," *Ultramicroscopy* **237**, 113517 (2022). [doi:10.1016/j.ultramic.2022.113517](https://doi.org/10.1016/j.ultramic.2022.113517)
- P. A. Midgley and A. S. Eggeman, "Precession electron diffraction — a topical review," *IUCrJ* **2**, 126–136 (2015). [doi:10.1107/S2052252514022283](https://doi.org/10.1107/S2052252514022283)
- Tutorial dataset source: precession 4D-STEM of a two-phase titanium alloy, *Journal of Microscopy* (2024). [doi:10.1111/jmi.13275](https://doi.org/10.1111/jmi.13275) · raw data: [University of Glasgow research data repository](https://doi.org/10.5525/gla.researchdata.1514)
