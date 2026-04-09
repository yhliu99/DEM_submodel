# MFDES: Multi-Frequency Deep Energy Submodeling for Localized High-Gradient Responses in Solid Mechanics

This repository hosts the research code and numerical examples for **MFDES** (Multi-Frequency Deep Energy Submodeling), a mesh-based deep energy framework for solid-mechanics problems with localized high-gradient or singular responses.

The method combines:

- **mesh-based energy integration**,
- a **mask-DOF strategy** for the strict enforcement of both physical and artificial boundaries, and
- a **two-stage global-local submodeling procedure** with **multi-frequency Fourier networks**.

In this way, the smooth global response and the localized high-gradient response can be resolved separately and coupled consistently within a unified deep energy setting.

## Highlights

- Unified treatment of **physical boundaries** and **artificial submodel boundaries** through the mask-DOF strategy
- **Finite-element-style Gaussian quadrature** embedded into a deep energy formulation
- **Two-stage submodeling** for separating smooth global behavior from localized singular/high-gradient behavior
- Support for both **strongly singular** and **weakly singular** solid-mechanics cases
- Natural extensibility to **multiple local submodels** and parallel workflows

## Numerical examples

The framework is assessed on four representative examples:

1. **Case 1: Boundary-enforcement verification**  
   Straight- and curved-boundary benchmarks for validating the mask-DOF boundary treatment.

2. **Case 2: Square plate under a concentrated load**  
   A strongly singular problem used to compare the proposed two-stage strategy with single-domain global-local baselines.

3. **Case 3: L-shaped beam with multiple local singularities**  
   A multi-source singular problem with two concentrated loads and a re-entrant corner.

4. **Case 4: Three-dimensional circular-hole plate**  
   A weakly singular 3D stress-concentration problem used to assess the applicability of MFDES to three-dimensional settings.

## Method overview

### 1. Mesh-based deep energy formulation
The displacement field is represented by a neural network, while the internal strain energy is evaluated through element-wise Gaussian quadrature on an integration mesh.

### 2. Mask-DOF boundary treatment
Boundary values are imposed directly at the degree-of-freedom level. This allows a unified and strict treatment of:

- physical Dirichlet boundaries, and
- artificial boundaries transferred from the global model to the local submodel.

### 3. Two-stage multi-frequency submodeling
- **Stage 1:** a coarse global model captures the smooth background response.
- **Stage 2:** a refined local submodel captures the localized high-gradient response.

Different Fourier settings can be used in the two stages so that the approximation capacity matches the response characteristics of each region.

## Repository status

This repository is currently **under active development**. The codebase may continue to evolve as the manuscript and numerical examples are further refined.

A recommended project layout is:

```text
.
├── cases/
│   ├── case1_boundary_enforcement/
│   ├── case2_single_singularity/
│   ├── case3_multiple_singularities/
│   └── case4_3d_hole/
├── src/
│   ├── models/
│   ├── mesh/
│   ├── energy/
│   ├── boundary/
│   ├── training/
│   └── postprocess/
├── data/
├── outputs/
├── figures/
└── README.md
```

## Suggested environment

A typical starting environment for this project is:

- Python 3.10+
- PyTorch
- NumPy
- SciPy
- pandas
- matplotlib
- openpyxl

You can later adapt this list to match the exact scripts that you decide to publish.

## Getting started

```bash
git clone <your-repo-url>
cd <your-repo-name>
python -m venv .venv
source .venv/bin/activate  # Linux/macOS
# .venv\Scripts\activate   # Windows
pip install -r requirements.txt
```

If you have not yet prepared `requirements.txt`, you can generate it after finalizing your environment.

## Citation

If you use this repository in academic work, please cite the associated manuscript:

```bibtex
@article{liu_mfdes,
  title   = {A Multi-Frequency Deep Energy Submodeling Framework for Localized High-Gradient Responses in Solid Mechanics},
  author  = {Liu, Yuhang and Ren, Huilong and Rabczuk, Timon and Zhuang, Xiaoying},
  note    = {Manuscript / preprint associated with this repository}
}
```

## License

This repository is released under the **MIT License** unless you choose to replace it with another license.

---

If you are publishing the official research code, you may also want to add later:

- `requirements.txt`
- `CITATION.cff`
- `environment.yml`
- example input data
- reproducible run scripts for each case
