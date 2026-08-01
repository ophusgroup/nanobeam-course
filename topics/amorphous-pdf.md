---
title: Amorphous materials & PDF
---

# Amorphous materials and pair distribution functions

**16:00 – 17:00 · Colin Ophus · Colab demo**

Glasses, amorphous thin films, liquids, and highly disordered solids have no unit cell — so the crystallographic toolkit of the morning sessions (Bragg disks, lattice vectors, orientation libraries) does not apply. But these materials are far from structureless: they have well-defined bond lengths, coordination shells, and often *medium-range order* (MRO) extending over 1–3 nm. This block covers how to quantify that structure from nanobeam diffraction.

## Describing disorder: n-body distribution functions

Without a lattice, structure is described statistically. The workhorse is the two-body **pair distribution function** g(r): the probability, relative to a random ideal gas, of finding an atom at distance *r* from another atom. Sharp peaks at the nearest-neighbor distance and progressively broader peaks at higher shells encode the local bonding; how quickly the oscillations decay measures the extent of order:

- A **nanocrystalline** material shows sharp, persistent peaks out to large *r*.
- A material with **medium-range order** shows a sharp first shell and damped oscillations that die out over a few nanometers.
- A **liquid or fully amorphous** structure shows a sharp minimum bond distance, a strong first shell, and essentially no structure beyond the second or third shell.

For multi-component systems the bookkeeping multiplies: two elements A and B produce three partial PDFs (A–A, B–B, A–B).

## Measuring the PDF with electron diffraction (ePDF)

Diffraction measures the Fourier transform of g(r). From a 4D-STEM dataset of an amorphous sample the workflow is:

1. **Polar transform.** Convert each diffraction pattern from Cartesian (kx, ky) to polar (φ, k) coordinates. This step is exquisitely sensitive to the pattern origin — an incorrect center produces wavy azimuthal artifacts that corrupt everything downstream. Automatic origin refinement (minimizing the standard deviation of intensity along the azimuthal direction at each probe position) makes this robust at scale.
2. **Azimuthal average → I(k).** Average over φ to get the radial scattering intensity.
3. **Background subtraction.** Fit and remove the smooth single-atom scattering background, e.g. with a model of the form

   $$B(k) = c + i_0 \exp\!\left(-\frac{k^2}{2 s_0^2}\right) + i_1 \exp\!\left(-\frac{k^4}{2 s_1^4}\right)$$

4. **Reduced structure factor.** Convert the background-corrected intensity to the reduced structure factor F(k) = k·(S(k) − 1).
5. **Sine transform → G(r).** A windowed sine transform of F(k) gives the reduced PDF G(r). Truncation of the k-range produces spurious low-r oscillations (atoms cannot be 0.5 Å apart!); damping schemes that iteratively fit S(k) and estimate the atomic number density ρ₀ suppress these artifacts.
6. **Normalize → g(r).** With the density in hand, $g(r) = 1 + \dfrac{G(r)}{4 \pi r \rho_0}$.

Because each step has failure modes, validation matters: in the tutorial we use a *simulated* 4D-STEM dataset of amorphous tantalum, so the measured g(r) can be compared against the ground-truth PDF computed directly from the atomic coordinates.

## Beyond the mean: mapping disorder in 4D

Unlike a selected-area or powder ePDF, a 4D-STEM measurement retains spatial resolution — each probe position carries its own diffuse-scattering signal, so you can *map* local structure:

- **Spatially resolved PDFs** distinguish amorphous phases, map crystalline/amorphous phase fractions, and track devitrification.
- **Fluctuation electron microscopy (FEM):** the *variance* of the diffracted intensity between probe positions (as a function of k and probe size) is sensitive to medium-range order that is invisible in the mean pattern.
- Angular correlation analyses of individual patterns can reveal local symmetry preferences in the glass.

## Practical notes

- Reach high enough k (several Å⁻¹) — camera length down, and mind the detector corners.
- Energy filtering removes the inelastic background and markedly improves S(k) at low k.
- Amorphous halos are also *useful*: fitting an ellipse to a carbon-film halo is a standard way to calibrate elliptical distortion for all the crystalline analyses too.

## Tutorial

:::{important}
🚧 **Google Colab notebook link coming soon.** The tutorial notebooks are being updated for the course and will be linked here.

In the meantime, see the [py4DSTEM tutorials repository](https://github.com/py4dstem/py4DSTEM_tutorials).
:::

## References

- D. J. H. Cockayne, "The Study of Nanovolumes of Amorphous Materials Using Electron Scattering," *Annual Review of Materials Research* **37**, 159–187 (2007). [doi:10.1146/annurev.matsci.35.082803.103337](https://doi.org/10.1146/annurev.matsci.35.082803.103337)
- M. M. J. Treacy, J. M. Gibson, L. Fan, D. J. Paterson, and I. McNulty, "Fluctuation microscopy: a probe of medium range order," *Reports on Progress in Physics* **68**, 2899 (2005). [doi:10.1088/0034-4885/68/12/R06](https://doi.org/10.1088/0034-4885/68/12/R06)
- P. M. Voyles and D. A. Muller, "Fluctuation microscopy in the STEM," *Ultramicroscopy* **93**, 147–159 (2002). [doi:10.1016/S0304-3991(02)00155-9](https://doi.org/10.1016/S0304-3991(02)00155-9)
- K. Yoshimoto and K. Omote, "Density estimation and origin-oscillation damping in electron pair distribution function analysis," *Journal of the Physical Society of Japan* **91**, 104602 (2022). [doi:10.7566/JPSJ.91.104602](https://doi.org/10.7566/JPSJ.91.104602)
- J. Ding and M. Asta, "Anisotropic structure and dynamics in metallic glass-forming liquids" (source of the amorphous Ta model used in the tutorial), *PNAS* **114** (2017). [doi:10.1073/pnas.1705723114](https://doi.org/10.1073/pnas.1705723114)
- C. Ophus, "Four-Dimensional Scanning Transmission Electron Microscopy (4D-STEM): From Scanning Nanodiffraction to Ptychography and Beyond," *Microscopy and Microanalysis* **25**, 563–582 (2019). [doi:10.1017/S1431927619000497](https://doi.org/10.1017/S1431927619000497)
