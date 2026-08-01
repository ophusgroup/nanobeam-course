---
title: Virtual & digital dark field
---

# Virtual dark field and digital dark field imaging

**13:00 – 13:45 · Ian MacLaren · Colab demo**

Because a 4D-STEM dataset contains the *entire* diffraction pattern at every probe position, any STEM detector geometry can be applied *after* the experiment: integrate the intensity inside a chosen region of the diffraction pattern at each probe position, and the result is an image. This is **virtual imaging**, and it is usually the first — and often the most informative — analysis applied to any 4D-STEM dataset.

## Virtual bright field and dark field

A circular mask over the central beam gives a virtual bright field (BF) image; an annulus outside it gives a virtual annular dark field (ADF). The two are complementary: electrons scattered out of the BF disk land in the DF detector, so regions that darken in BF brighten in DF. Unlike physical detectors, virtual detectors are free — you can try any inner/outer radius, any shape, any position, and iterate until the contrast isolates the feature you care about:

- **Detector design matters.** The BF detector should capture the unscattered disk (slightly expanded to tolerate residual descan); the ADF annulus geometry controls whether contrast is dominated by diffraction (low angles) or thickness/Z (high angles).
- **Selected-area diffraction in reverse:** integrating diffraction patterns over a *real-space* region of interest gives a virtual selected-area pattern from exactly that region — ideal for identifying which reflections belong to which microstructural feature.

## Digital dark field

Classical dark field TEM tilts the beam so one chosen Bragg reflection passes the objective aperture. The 4D-STEM equivalent — **digital dark field (DDF)** — places a virtual aperture over one (or several) specific Bragg reflections and maps where in real space that reflection is excited. This is enormously powerful for microstructure:

- **Grain and domain mapping:** each grain lights up only in the reflections it produces, so DDF images segment grains, twins, and ferroelastic/ferroelectric domains — even when they are invisible in BF/ADF contrast.
- **Superlattice and ordered phases:** placing the aperture on superlattice reflections maps ordered regions and antiphase domains directly.
- **Tracking spots, not just masking them:** in real datasets the reflections move (strain, rotation, descan), so robust DDF implementations follow the peak within a window rather than using a fixed mask — this is where the Bragg-vector-based approaches and fast implementations (e.g., Kelvin_STEM, py4DSTEM, pyxem) come in.
- From the ensemble of DDF images, phase and domain maps of the whole field of view can be assembled — the manual counterpart of the [ML clustering approaches](./ml-clustering.md) in the next block.

## Tutorial

:::{important}
🚧 **Google Colab notebook link coming soon.** The tutorial notebooks are being updated for the course and will be linked here.

In the meantime, see the [py4DSTEM tutorials repository](https://github.com/py4dstem/py4DSTEM_tutorials).
:::

## References

- C. Gammer et al., "Diffraction contrast imaging using virtual apertures," *Ultramicroscopy* **155**, 1–10 (2015). [doi:10.1016/j.ultramic.2015.03.015](https://doi.org/10.1016/j.ultramic.2015.03.015)
- G. W. Paterson et al., "Fast Pixelated Detectors in Scanning Transmission Electron Microscopy. Part II: Post-Acquisition Data Processing, Visualization, and Structural Characterization," *Microscopy and Microanalysis* **26**, 944–963 (2020). [doi:10.1017/S1431927620024307](https://doi.org/10.1017/S1431927620024307)
- I. MacLaren et al., "A Comparison of a Direct Electron Detector and a High-Speed Video Camera for a Scanning Precession Electron Diffraction Phase and Orientation Mapping," *Microscopy and Microanalysis* **26**, 1110–1116 (2020). [doi:10.1017/S1431927620024411](https://doi.org/10.1017/S1431927620024411)
- C. Ophus, "Four-Dimensional Scanning Transmission Electron Microscopy (4D-STEM): From Scanning Nanodiffraction to Ptychography and Beyond," *Microscopy and Microanalysis* **25**, 563–582 (2019). [doi:10.1017/S1431927619000497](https://doi.org/10.1017/S1431927619000497)
