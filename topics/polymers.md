---
title: Semicrystalline polymers
---

# Orientation and flowline mapping of semicrystalline polymers

**15:00 – 16:00 · Stephanie Ribet · Colab demo**

Semicrystalline polymers and small-molecule organic films — conjugated polymers for organic electronics, polyolefins, peptide and protein assemblies — derive their properties from nanoscale crystalline domains embedded in an amorphous matrix. Charge transport in an organic semiconductor, for example, depends on how the π-stacking direction of crystallites connects across the film. These materials are essentially impossible to characterize by conventional high-resolution imaging: they are extremely beam sensitive, with critical fluences of order 1–100 e⁻/Å², destroyed long before an atomic-resolution image can be formed.

Nanobeam 4D-STEM sidesteps this. Diffraction concentrates the structural information from the whole illuminated volume into a few sharp features, so a useful diffraction pattern can be recorded with orders of magnitude fewer electrons than an image — and with a fast camera, the dose is spread over the full field of view in a single low-fluence pass.

## From diffraction patterns to orientation maps

Polymer crystallites typically produce a strong, characteristic reflection (e.g., the ~3.6 Å π–π stacking peak in P3HT, or lamellar/backbone reflections at lower angles). The workflow:

1. **Detect the arcs.** At each probe position, locate the azimuthal position of the characteristic reflection — polymer patterns show arcs rather than sharp spots because of local disorder. Polar transformation of each pattern makes the azimuthal intensity distribution easy to fit.
2. **Map orientation.** The azimuthal angle of the arc gives the local crystallite orientation (modulo the symmetry of the reflection); its intensity gives the degree of crystallinity/alignment. The result is an orientation field over the scanned area.
3. **Draw flowlines.** Orientation fields are hard to read as color maps alone. **Flowline maps** — streamlines integrated through the orientation vector field, drawn with density proportional to local alignment — render the connectivity of the crystalline regions directly, in images reminiscent of van Gogh's *Starry Night*. Connectivity, domain size, and defect structures (disclinations, grain boundaries in the orientation field) become immediately visible.

## Dose-limited experiment design

Everything about these experiments is a dose budget negotiation:

- **Total fluence** must stay below the damage threshold — measure the critical dose for your material first (e.g., by watching a reflection fade under repeated exposure).
- **Step size vs. probe size:** large scan steps (often ≫ probe size) spread the dose; the orientation field is smooth enough that sparse sampling still captures it.
- **Cryo helps:** cooling typically increases critical dose by a factor of a few.
- **Detector:** electron counting and high frame rates let you work at the shot-noise limit; pattern-level denoising and radial-symmetry priors can be applied in analysis.

## Tutorial

:::{important}
🚧 **Google Colab notebook link coming soon.** The tutorial notebooks are being updated for the course and will be linked here.

In the meantime, see the [py4DSTEM tutorials repository](https://github.com/py4dstem/py4DSTEM_tutorials).
:::

## References

- O. Panova et al., "Diffraction imaging of nanocrystalline structures in organic semiconductor molecular thin films," *Nature Materials* **18**, 860–865 (2019). [doi:10.1038/s41563-019-0387-3](https://doi.org/10.1038/s41563-019-0387-3)
- K. C. Bustillo, S. E. Zeltmann et al., "4D-STEM of Beam-Sensitive Materials," *Accounts of Chemical Research* **54**, 2543–2551 (2021). [doi:10.1021/acs.accounts.1c00073](https://doi.org/10.1021/acs.accounts.1c00073)
- O. Panova et al., "Orientation mapping of semicrystalline polymers using scanning electron nanobeam diffraction," *Micron* **88**, 30–36 (2016). [doi:10.1016/j.micron.2016.05.008](https://doi.org/10.1016/j.micron.2016.05.008)
- 🚧 Additional recent low-dose 4D-STEM soft-matter references will be added along with the course tutorial links.
