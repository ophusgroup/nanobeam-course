---
title: Strain mapping
---

# Strain mapping with nanobeam electron diffraction


```{image} ../assets/cover-strain.jpg
:alt: Schematic of nanobeam strain mapping — a converged probe scanned over a strained crystal produces diffraction patterns whose Bragg disk positions encode the local lattice vectors
:width: 100%
```

Strain — the local deviation of the lattice from its relaxed spacing — controls band structure in semiconductor devices, mobility in strained channels, ferroelastic domain patterns, and mechanical response around defects and precipitates. Nanobeam electron diffraction (NBED) strain mapping measures it directly: the positions of the Bragg disks in each diffraction pattern encode the local reciprocal lattice vectors, so tracking how disk positions shift as the probe scans across the sample gives the full 2D strain tensor — ε<sub>xx</sub>, ε<sub>yy</sub>, ε<sub>xy</sub>, and lattice rotation θ — at every probe position, over fields of view of microns with nanometer resolution.

## How it works

1. **Probe template.** Record a vacuum probe image (or extract a template from a thin region of the dataset). Its cross-correlation kernel — typically shaped with a sigmoid edge — is what makes disk detection precise.
2. **Bragg disk detection.** Cross-correlate the template with every diffraction pattern and locate the correlation maxima with subpixel precision. In py4DSTEM this is `find_Bragg_disks`; the key hyperparameters are the correlation power, minimum peak intensity/spacing, and the subpixel mode (`'poly'` is fast for tutorials; **`'multicorr'` is recommended for high-precision strain mapping**).
3. **Calibration.** Correct the origin (descan), elliptical distortion, and the real-space/reciprocal-space rotation — see the [data handling module](./data-handling.md). Calibration errors map directly into artificial strain.
4. **Lattice fitting.** Choose basis vectors *g*₁ and *g*₂ from the Bragg vector map (ideally perpendicular, well-separated reflections), and fit the full lattice at every probe position.
5. **Strain from a reference.** Strain is always measured *relative to a reference lattice* — either the median lattice over a region of interest known to be unstrained, or manually specified reference vectors (e.g., from theory). The transformation between the local and reference lattice vectors, rotated into your chosen coordinate system, gives ε<sub>xx</sub>, ε<sub>yy</sub>, ε<sub>xy</sub>, and θ.

## Precision and pitfalls

- Disk registration precision improves with sharp, uniform disk edges — this is where convergence angle, sample thickness (dynamical contrast inside the disks), and patterned "bullseye" probes matter. Precision of ~10⁻⁴ relative strain is achievable in favorable cases; a few ×10⁻³ is routine.
- Thickness and mistilt vary across real samples and modulate the intensity *inside* disks, which can bias center-fitting; robust registration algorithms and (where available) precession help.
- The choice of reference region is a physics decision, not a software one: strain maps are only as meaningful as the reference lattice they are measured against.
- Useful derived quantities: the *strain dilation* ε<sub>xx</sub> + ε<sub>yy</sub> (volumetric part), and statistics of strain over segmented regions (e.g., precipitates vs. matrix) via masks and histograms.

## Tutorial

:::{important}
🚧 **Google Colab notebook link coming soon.** The tutorial notebooks are being updated for the course and will be linked here.

In the meantime, see the [py4DSTEM tutorials repository](https://github.com/py4dstem/py4DSTEM_tutorials).
:::

## References

- V. B. Ozdol et al., "Strain mapping at nanometer resolution using advanced nano-beam electron diffraction," *Applied Physics Letters* **106**, 253107 (2015). [doi:10.1063/1.4922994](https://doi.org/10.1063/1.4922994)
- T. C. Pekin et al., "Optimizing disk registration algorithms for nanobeam electron diffraction strain mapping," *Ultramicroscopy* **176**, 170–176 (2017). [doi:10.1016/j.ultramic.2016.12.021](https://doi.org/10.1016/j.ultramic.2016.12.021)
- S. E. Zeltmann et al., "Patterned probes for high precision 4D-STEM Bragg measurements," *Ultramicroscopy* **209**, 112890 (2020). [doi:10.1016/j.ultramic.2019.112890](https://doi.org/10.1016/j.ultramic.2019.112890)
- A. Béché et al., "Strain measurement at the nanoscale: Comparison between convergent beam electron diffraction, nano-beam electron diffraction, high resolution imaging and dark field electron holography," *Ultramicroscopy* **131**, 10–23 (2013). [doi:10.1016/j.ultramic.2013.03.014](https://doi.org/10.1016/j.ultramic.2013.03.014)
- M. J. Hÿtch, E. Snoeck, and R. Kilaas, "Quantitative measurement of displacement and strain fields from HREM micrographs," *Ultramicroscopy* **74**, 131–146 (1998). [doi:10.1016/S0304-3991(98)00035-7](https://doi.org/10.1016/S0304-3991(98)00035-7) — the geometric phase analysis (GPA) counterpart to NBED strain mapping.
- K. Ma et al., "Nanoscale characterization of irradiation effects in a ferritic alloy" (strain mapping application example), *Acta Materialia* (2025). [doi:10.1016/j.actamat.2025.121095](https://doi.org/10.1016/j.actamat.2025.121095)
