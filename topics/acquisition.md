---
title: Acquiring nanobeam diffraction data
---

# Practical guidance for nanobeam 4D-STEM acquisition

**8:30 – 9:15 · All instructors · Slides**

In four-dimensional scanning transmission electron microscopy (4D-STEM), we scan a focused or nearly-parallel electron probe over a two-dimensional grid of positions on the sample, and record a full two-dimensional diffraction pattern at every position. The result is a four-dimensional dataset: two real-space scan dimensions and two reciprocal-space detector dimensions. Almost every analysis in this course — strain mapping, orientation mapping, virtual imaging, polymer orientation, pair distribution functions — starts from the same kind of measurement, and the quality of every one of them is set at the microscope, before any software is involved.

This opening block covers the practical decisions that determine whether a nanobeam experiment succeeds.

## The fundamental trade-off: probe size vs. angular resolution

The convergence semi-angle α of the probe controls both the real-space probe size and the size of the diffracted Bragg disks. A large convergence angle gives a small probe (better spatial resolution) but large, potentially overlapping disks; a small convergence angle gives sharp, well-separated diffraction spots but a wider probe. Diffraction disks overlap when 2α exceeds the Bragg angle separation of adjacent reflections, so for disk-registration methods such as strain mapping we typically choose α of a fraction of a milliradian up to a few milliradians — the "nanobeam" regime, with probe sizes of roughly 1–5 nm.

Things to consider when choosing probe conditions:

- **Convergence angle:** small enough that disks of interest do not overlap, large enough that the probe stays small compared to the microstructural features you want to resolve. Disk-edge sharpness also sets how precisely disk positions can be measured.
- **Probe current and dose:** diffraction disk registration works well even at low dose, but weak reflections (superlattice peaks, high-order Laue zones, amorphous halos) need adequate counts. For beam-sensitive materials (see the [polymer block](./polymers.md)), total fluence budgets of 1–100 e⁻/Å² may apply, which dictates probe current, dwell time, and step size.
- **Scan step size:** for mapping, the step is usually chosen comparable to or larger than the probe size. Oversampling wastes dose; undersampling misses microstructure.
- **Camera length:** sets which scattering angles land on the detector. Strain and orientation mapping want the first few orders of Bragg reflections; PDF measurements want to reach high scattering vectors (k of several Å⁻¹).
- **Energy filtering:** zero-loss filtering of diffraction patterns substantially improves the background for PDF and fluctuation microscopy measurements on thicker samples.

## Detectors and cameras

Modern 4D-STEM is enabled by fast direct electron detectors. Relevant camera parameters:

- **Frame rate** sets the total acquisition time: a 512×512 real-space scan at 1 kHz takes over four minutes — long enough that sample drift and contamination matter. Modern detectors run from ~1 kHz (hybrid pixel array detectors) up to ~100 kHz (thin active pixel sensors).
- **Dynamic range:** the unscattered central beam can be 10⁴–10⁶ times more intense than the weakest features of interest. High-dynamic-range detectors (or a beamstop, or patterned/bullseye apertures) prevent saturation.
- **Detector counts and noise:** electron-counting detectors give Poisson-limited data, which is what makes low-dose diffraction analysis quantitative.

## Practical checklist

1. Align the microscope in TEM/STEM mode and select the nanobeam aperture (often a 10–50 μm condenser aperture, or a dedicated microprobe mode).
2. Check the probe in real space (size, shape) *and* the diffraction pattern (disk sharpness) before starting a scan.
3. Set camera length so all reflections of interest fall on the detector — check the corners, not just the center.
4. Verify counts: no saturation in the central beam, adequate signal in the weakest disks you need.
5. Acquire calibration data: a vacuum probe image (for disk-template methods), a known calibration standard (e.g., gold nanoparticles) for pixel size and elliptical distortion, and a scan-rotation calibration.
6. Record all metadata — accelerating voltage, camera length, convergence angle, dwell time, probe current — your future self doing the analysis will thank you.

## Slides

:::{note}
🚧 The slide deck for this session will be posted here after the course.
:::

## References

- C. Ophus, "Four-Dimensional Scanning Transmission Electron Microscopy (4D-STEM): From Scanning Nanodiffraction to Ptychography and Beyond," *Microscopy and Microanalysis* **25**, 563–582 (2019). [doi:10.1017/S1431927619000497](https://doi.org/10.1017/S1431927619000497)
- S. Nord et al., "Fast Pixelated Detectors in Scanning Transmission Electron Microscopy. Part I: Data Acquisition, Live Processing, and Storage," *Microscopy and Microanalysis* **26**, 653–666 (2020). [doi:10.1017/S1431927620001713](https://doi.org/10.1017/S1431927620001713)
- G. W. Paterson et al., "Fast Pixelated Detectors in Scanning Transmission Electron Microscopy. Part II: Post-Acquisition Data Processing, Visualization, and Structural Characterization," *Microscopy and Microanalysis* **26**, 944–963 (2020). [doi:10.1017/S1431927620024307](https://doi.org/10.1017/S1431927620024307)
- M. W. Tate et al., "High Dynamic Range Pixel Array Detector for Scanning Transmission Electron Microscopy," *Microscopy and Microanalysis* **22**, 237–249 (2016). [doi:10.1017/S1431927615015664](https://doi.org/10.1017/S1431927615015664)
- S. E. Zeltmann et al., "Patterned probes for high precision 4D-STEM Bragg measurements," *Ultramicroscopy* **209**, 112890 (2020). [doi:10.1016/j.ultramic.2019.112890](https://doi.org/10.1016/j.ultramic.2019.112890)
- K. C. Bustillo, S. E. Zeltmann et al., "4D-STEM of Beam-Sensitive Materials," *Accounts of Chemical Research* **54**, 2543–2551 (2021). [doi:10.1021/acs.accounts.1c00073](https://doi.org/10.1021/acs.accounts.1c00073)
