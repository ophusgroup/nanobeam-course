---
title: Data handling & calibration
---

# Loading, organizing, and calibrating 4D-STEM data

**9:45 – 10:00 · Stephanie Ribet · Colab demo**

Before any physics can come out of a 4D-STEM dataset, the data has to be loaded, organized, and — critically — calibrated. This short demo walks through the py4DSTEM data pipeline: reading files, browsing the 4D datacube interactively, and applying the chain of calibrations that turn detector pixels into physical units.

## Loading data across formats

4D-STEM data arrives in many containers: vendor formats (Gatan `.dm4`, Thermo Fisher `.emd`/velox, DECTRIS, Merlin/Medipix `.mib`, EMPAD raw), community HDF5 layouts (EMD 1.0), and plain arrays (`.npy`/`.npz`). py4DSTEM reads most of these directly with `py4DSTEM.import_file` / `py4DSTEM.read`, and any NumPy array can be wrapped into a `DataCube`:

```python
import py4DSTEM
datacube = py4DSTEM.import_file("experiment.dm4")

# or, from a raw array:
import numpy as np
data = np.load("scan.npz")["arr_0"]     # shape (Rx, Ry, Qx, Qy)
datacube = py4DSTEM.DataCube(data=data)
```

The four dimensions are conventionally ordered `(Rx, Ry, Qx, Qy)`: two real-space scan coordinates, then two reciprocal-space detector coordinates. Analysis products (mean patterns, virtual images, Bragg peaks, calibrations) are stored alongside the data in a tree structure that can be saved to and reloaded from HDF5 — which also means expensive intermediate results (like Bragg disk detection over millions of patterns) can be checkpointed and shared.

## Browsing the datacube

The first thing to do with any new dataset is *look at it*. Scrubbing through diffraction patterns as a function of probe position builds intuition about what is in the data — where the vacuum is, which regions are crystalline, how much the pattern changes between neighboring positions — and immediately reveals problems like detector saturation or beam damage. In the demo we use an interactive 4D browser to explore the dataset live; the mean and maximum diffraction patterns computed over all probe positions give a compact overview of everything the detector saw.

## The calibration chain

A useful mental model: every measurement we make in this course is a *position* or *intensity* in the diffraction pattern, so every distortion of the diffraction pattern propagates directly into the physics. The standard calibration chain in py4DSTEM is:

1. **Pixel sizes.** The real-space step size (from the scan settings) and the reciprocal-space pixel size (from the camera length, or better, measured from a known reference — see below). Always sanity-check the scale bars on your virtual images afterwards.
2. **Origin / descan correction.** The center of the diffraction pattern shifts as the beam scans, due to imperfect descan alignment. A classic signature: the central disk in the *maximum* diffraction pattern looks like a rounded rectangle — the circular center disk convolved with the rectangle traced out by the descan across the scan. We measure the origin at every probe position (`measure_origin`) and fit a smooth plane or low-order polynomial to it (`fit_origin`, with robust fitting to suppress outliers).
3. **Elliptical distortion.** Projector lens distortions and detector tilt stretch the diffraction pattern into a slight ellipse. This can be measured from the amorphous halo of a carbon support film (fitting an ellipse to the ring) or from a standard sample, then corrected with `set_p_ellipse`.
4. **Real-space ↔ reciprocal-space rotation.** The scan direction and detector axes are rotated relative to each other (scan coils and camera each have their own orientation), and data can additionally be transposed on read-in. This rotation must be measured — for example with a center-of-mass (DPC-style) analysis of the center beam, where a correct rotation produces clean dipole contrast along x in CoMx and along y in CoMy — and set with `set_QR_rotation_degrees` / `set_QR_flip`. Getting this wrong rotates your strain tensor and orientation maps!
5. **Pixel size against a known structure.** For quantitative work, the reciprocal pixel size can be refined by comparing measured Bragg peak positions against structure factors calculated from a known reference crystal (e.g., from a CIF file), overlaying simulated and measured radial scattering intensity.

:::{tip}
Record a vacuum probe image in every session. It provides the template for Bragg disk detection, measures the convergence angle, and captures the true probe shape. If you forget, a synthetic probe or a template extracted from a thin sample region can substitute — but it's never as good.
:::

## Tutorial

:::{important}
🚧 **Google Colab notebook link coming soon.** The tutorial notebooks are being updated for the course and will be linked here.

In the meantime, see the [py4DSTEM tutorials repository](https://github.com/py4dstem/py4DSTEM_tutorials).
:::

## References

- B. H. Savitzky et al., "py4DSTEM: A Software Package for Four-Dimensional Scanning Transmission Electron Microscopy Data Analysis," *Microscopy and Microanalysis* **27**, 712–743 (2021). [doi:10.1017/S1431927621000477](https://doi.org/10.1017/S1431927621000477)
- C. Ophus, "Four-Dimensional Scanning Transmission Electron Microscopy (4D-STEM): From Scanning Nanodiffraction to Ptychography and Beyond," *Microscopy and Microanalysis* **25**, 563–582 (2019). [doi:10.1017/S1431927619000497](https://doi.org/10.1017/S1431927619000497)
- S. Nord et al., "Fast Pixelated Detectors in Scanning Transmission Electron Microscopy. Part I: Data Acquisition, Live Processing, and Storage," *Microscopy and Microanalysis* **26**, 653–666 (2020). [doi:10.1017/S1431927620001713](https://doi.org/10.1017/S1431927620001713)
- G. W. Paterson et al., "Fast Pixelated Detectors in Scanning Transmission Electron Microscopy. Part II: Post-Acquisition Data Processing, Visualization, and Structural Characterization," *Microscopy and Microanalysis* **26**, 944–963 (2020). [doi:10.1017/S1431927620024307](https://doi.org/10.1017/S1431927620024307)
