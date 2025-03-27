# Elasticity Problem Solving using Computer Aided Engineering Modelling

## Overview

This project presents a numerical analysis of a 2D static elasticity problem applied to a bow tie structure using FreeFEM++. The objective is to investigate the displacement field and stress distribution under symmetric mechanical loading, with a focus on identifying stress concentration regions and validating the numerical approach via finite element modelling.

## Table of Contents

- [Overview](#overview)
- [Problem Description](#problem-description)
- [Finite Element Analysis](#finite-element-analysis)
- [Results and Visualizations](#results-and-visualizations)
- [Project Structure](#project-structure)
- [Installation and Usage](#installation-and-usage)
- [Future Work](#future-work)
- [License](#license)
- [Acknowledgements](#acknowledgements)

## Problem Description

The analysis is conducted on a bow tie structure characterized by:

- **Geometry:** 
  - Side length: `a = 10 m`
  - Internal angle: `60°`
  
- **Boundary Conditions:**
  - **Dirichlet (Fixed):**
    - Left edge (`x = -a/2`): Horizontal displacement (`u1 = 0`)
    - Bottom edge (along `y = -tan(60°)|x|`): Vertical displacement (`u2 = 0`)
  - **Neumann (Applied Stresses):**
    - Right edge (`x = a/2`): Horizontal stress (`Sx = 10 MPa`)
    - Top edge (along `y = tan(60°)|x|`): Vertical stress (`Sy = 10 MPa`)

The goal is to determine the displacement field and stress distribution, including the von Mises stress, to pinpoint regions with potential failure risks.

## Finite Element Analysis

- **Mesh:**  
  A structured triangular mesh with 20 nodes per edge is generated to ensure sufficient resolution for linear shape functions (P1).

- **Weak Formulation:**  
  The linear elasticity problem is formulated as:

  \[
  \int_{\Omega} \sigma(u) : \epsilon(v) \, d\Omega = \int_{\partial \Omega} t \cdot v \, d\Gamma \quad \forall v \in V,
  \]

  where:

  - \(\sigma(u) = \lambda \, \text{tr}(\epsilon) I + 2G\epsilon\) is the stress tensor.
  - \(\epsilon = \frac{1}{2} (\nabla u + \nabla u^T)\) is the strain tensor.
  - \(V\) is the space of admissible displacements with the imposed Dirichlet conditions.

## Results and Visualizations

The simulation provides key visual outputs including:

- **Deformation Field:**  
  Displays the displacement field (scaled for clarity) showing significant horizontal and vertical motion, particularly near the loaded edges.

- **Stress Distributions:**  
  - **\(\sigma_{xx}\):** Highest near the fixed left edge.
  - **\(\sigma_{yy}\):** Concentrated near the fixed bottom edge.
  - **\(\sigma_{xy}\):** Peaks at the corners indicating high shear stress.
  - **Von Mises Stress:** Highlights critical regions near the constrained boundaries.

## Project Structure

```
├── README.md
├── elasticity_bowtie.edp       # FreeFEM++ script for simulation
├── output.dat                  # Computed stress and displacement data
└── figures
    ├── mesh.eps                # Mesh visualization
    ├── deformed.eps            # Deformed configuration visualization
    ├── displacement.eps        # Displacement vector field
    ├── sigmaxx.eps             # \(\sigma_{xx}\) stress distribution
    ├── sigmayy.eps             # \(\sigma_{yy}\) stress distribution
    ├── sigmaxy.eps             # \(\sigma_{xy}\) stress distribution
    └── vonMises.eps            # Von Mises stress distribution
```

## Installation and Usage

### Prerequisites

- [FreeFEM++](https://freefem.org/) must be installed.
- A Unix-like environment (Linux, macOS) or Windows with a compatible shell.

### Running the Simulation

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/elasticity-problem-solving.git
   cd elasticity-problem-solving
   ```

2. **Execute the FreeFEM++ Script:**
   ```bash
   FreeFem++ elasticity_bowtie.edp
   ```

3. **Review the Results:**  
   Check the `output.dat` file and view the generated figures in the `figures` folder.

## Future Work

- **Mesh Refinement:**  
  Incorporate adaptive mesh refinement, especially near stress concentration areas.

- **Extended Loading Conditions:**  
  Investigate additional loading scenarios such as shear, bending, or combined stresses.

- **Higher-Order Elements:**  
  Explore the use of higher-order finite elements to improve accuracy.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgements

- Developed by **Nodira Tillayeva**.
- The analysis and simulations are performed using [FreeFEM++](https://freefem.org/).
