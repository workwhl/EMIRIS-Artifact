# EMIRIS: Partial Artifact and Demo Samples

This repository provides a partial research artifact for the paper:

> **Toward Iris Eavesdropping via Electromagnetic Side Channels in Near-Infrared Sensing Systems**

EMIRIS demonstrates that unintended electromagnetic (EM) emissions produced during the digital readout and transmission of near-infrared (NIR) iris sensors can reveal structured iris information. The released artifact contains representative EM recordings and their corresponding reconstruction outputs to support inspection of the relationship between the captured leakage and the recovered iris patterns.

## Scope of This Release

This is a **limited artifact release**, rather than a complete release of the EMIRIS system. It is intended to support reproducibility assessment and qualitative examination of representative trace-to-output examples.

The repository includes:

- Representative raw baseband EM recordings captured during active iris acquisition.
- Initial iris matrices reconstructed from the EM recordings.
- Final iris images reconstructed by the complete EMIRIS pipeline.

The repository does **not** include:

- The complete EM recording dataset.
- The full attack implementation or automated end-to-end pipeline.
- Diffusion-model training data, model weights, or training code.
- Personally identifying participant information.

## Repository Structure

```text
EMIRIS-Artifact/
├── README.md
└── sample/
    ├── raw_em.npy
    ├── Raw.jpg
    └── Rec.jpg
```

Each sample contains only the following three files:

- `raw_em.npy`: one-dimensional complex baseband I/Q samples stored as a NumPy `complex64` array.
- `Raw.jpg`: initial iris matrix produced by EM Emissions-to-Iris Matrix Mapping (EIM).
- `Rec.jpg`: final iris image produced by the complete EIM, Iris Data Enhancement (IDE), and Iris Denoising and Detail Generation (IDG) pipeline.

## Experimental Configuration

The representative recordings were collected using the experimental platform described in the paper.

| Component | Configuration |
|---|---|
| Software-defined radio | USRP X310 |
| RF daughterboard | UBX-160 |
| Short-range antenna | FOSTTEK NFP-ONE near-field magnetic antenna |
| Longer-range antenna | HTOOL HT8 directional antenna |
| Low-noise amplifier | FOSTTEK FST-RFAMP06 |
| Default LNA gain | 40 dB |
| Default BPF bandwidth | 5 MHz |
| Default sampling rate | 20 MS/s |
| Acquisition software | GNU Radio 3.10.7.0 |
| Operating system | Ubuntu 24.04.4 |

The dominant leakage band is hardware-configuration-specific. It is identified by scanning the target device over 100-2000 MHz, ranking spectral peaks observed during active iris acquisition, and validating their frame- and row-level periodicity. Once identified for a hardware configuration, the center frequency can be reused across users and capture sessions.

The two corresponding PNG files provide a direct comparison between the initial reconstruction and the final EMIRIS output. They are provided for inspection only; the complete reconstruction pipeline is not part of this limited release.

## Interpreting the Released Outputs

- **Initial reconstruction:** preserves the coarse spatial organization derived from the sensor's sequential row and column transmission, but may contain blur, intensity distortion, and incomplete texture mapping.
- **Final reconstruction:** combines IDE and IDG to improve structural continuity and visual fidelity while using the EM-derived condition to anchor the restored iris pattern to the source observation.

The released examples should not be interpreted as evidence that two-dimensional reconstructed images can bypass presentation-attack or liveness-detection systems. The demonstrated scope concerns iris-information disclosure and recognition systems without effective liveness checks.

## Reproducibility Notes

- The target NIR device must be actively acquiring and transmitting iris frames during EM recording.
- The center frequency must be identified once for each previously unseen hardware configuration.
- The default BPF bandwidth and LNA gain used in the paper are 5 MHz and 40 dB, respectively.
- Reconstruction quality depends on the received signal-to-noise ratio, antenna placement, distance, intervening materials, and in-band interference.
- This artifact supports examination of representative recordings and outputs, but does not reproduce every experiment or result reported in the paper.

## Data Sensitivity and Responsible Use

Iris information is sensitive biometric data. This repository therefore contains only a limited set of representative research samples and excludes direct participant identifiers. The materials are provided solely for academic evaluation, reproducibility assessment, and defensive research. They must not be used to target biometric systems or individuals without explicit authorization.

## License

Unless otherwise stated, all materials in this repository remain copyrighted by the authors. Making these representative files available for research evaluation does not grant permission for commercial use, redistribution, or deployment against real-world systems.

## Citation

If you use this artifact in academic work, please cite:

```text
Wenhao Li et al., "Toward Iris Eavesdropping via Electromagnetic
Side Channels in Near-Infrared Sensing Systems," IEEE Transactions
on Mobile Computing.
```

The complete bibliographic information will be updated after publication.
