# Chemical Engineering Aspects of Green Hydrogen Production via PEM Electrolysis Visualization

**Date:** May 2, 2025
**Authors:** Lokesh Gottapu (M.Sc. CEE), Sai Teja Dampanaboina (M.Sc. Informatik), Syed Muhammad Abdul Basit (M.Sc. CEE)
**Supervisors:** Dr.-Ing. Nicole Vorhauer (FVST), Dr.-Ing. David Broneske (FIN)

## Table of Contents

* [Introduction](#introduction)

  * [Project Context and Motivation](#project-context-and-motivation)
  * [Project Goal and Collaboration](#project-goal-and-collaboration)
  * [Scope of Chemical Engineering Contribution](#scope-of-chemical-engineering-contribution)
  * [Importance of Visualization](#importance-of-visualization)
* [PEM Electrolysis Fundamentals I: The Electrochemical Core](#pem-electrolysis-fundamentals-i-the-electrochemical-core)

  * [Overall Reaction](#overall-reaction)
  * [Electrode Half‑Reactions](#electrode-half-reactions)
  * [Proton Exchange Membrane (PEM)](#proton-exchange-membrane-pem)
  * [Membrane Electrode Assembly (MEA)](#membrane-electrode-assembly-mea)
  * [Bipolar/Flow Field Plates](#bipolarflow-field-plates)
* [Process Description I: System Layout & Core Unit](#process-description-i-system-layout--core-unit)

  * [System Boundaries](#system-boundaries)
  * [Simplified Process Flow Diagram (PFD)](#simplified-process-flow-diagram-pfd)
  * [Feed Water Requirements](#feed-water-requirements)
  * [PEM Electrolyzer Stack](#pem-electrolyzer-stack)
* [Technical Calculations I: Stoichiometry & Production Rate](#technical-calculations-i-stoichiometry--production-rate)

  * [Basis of Calculation](#basis-of-calculation)
  * [Stoichiometry](#stoichiometry)
  * [Faraday’s Laws & Efficiency](#faradays-laws--efficiency)
  * [Actual Production Rate](#actual-production-rate)
* [PEM Electrolysis Fundamentals II: Performance Factors](#pem-electrolysis-fundamentals-ii-performance-factors)

  * [Thermodynamics](#thermodynamics)
  * [Kinetics & Overpotentials](#kinetics--overpotentials)
  * [Key Influencing Factors](#key-influencing-factors)
* [Technical Calculations II: Voltage, Energy & Efficiency](#technical-calculations-ii-voltage-energy--efficiency)

  * [Cell & Stack Voltage](#cell--stack-voltage)
  * [Energy Consumption](#energy-consumption)
  * [Efficiency Definitions](#efficiency-definitions)
  * [Heat Generation](#heat-generation)
  * [Key Visualized Aspects](#key-visualized-aspects)
  * [Assumptions & Simplifications](#assumptions--simplifications)
* [App Development](#app-development)

  * [Development Tools](#development-tools)
  * [Application Structure](#application-structure)
  * [Usage](#usage)
  * [Implementation Highlights](#implementation-highlights)
* [Conclusion & Future Work](#conclusion--future-work)

  * [Summary of Contributions](#summary-of-contributions)
  * [Significance & Challenges](#significance--challenges)
  * [Future Work Suggestions](#future-work-suggestions)
* [References](#references)

---

## Introduction

### Project Context and Motivation

Green hydrogen—produced by water electrolysis using renewable energy—is key to decarbonizing transport, industry, and power. PEM electrolysis offers high efficiency, fast response, compact design, and pure H₂ output, but its principles and integration can be complex.

### Project Goal and Collaboration

Develop an interactive educational tool (Unity + Blender) to visualize green hydrogen production via PEM electrolysis. Joint effort between the Faculties of Computer Science (FIN) and Process & Systems Engineering (FVST).

### Scope of Chemical Engineering Contribution

* Detailed electrochemical theory
* Process system design (flowsheet, Balance of Plant)
* Quantitative models: production rates, voltages, energy, efficiency
* Translation of technical data into clear visual cues

### Importance of Visualization

Interactive 3D scenes enable exploration of microscale processes (ion transport, catalysis) and macroscale plant layout, illustrating cause–effect (e.g., current density vs. output) far better than static diagrams.

## PEM Electrolysis Fundamentals I: The Electrochemical Core

### Overall Reaction

```
H₂O(l) + Electrical Energy → H₂(g) + ½ O₂(g)   (ΔH°₃₀₀K ≈ 286 kJ/mol H₂)
```

### Electrode Half‑Reactions

* **Anode (Oxidation):**
  H₂O → 2H⁺ + ½O₂ + 2e⁻  (E° = +1.23 V)
* **Cathode (Reduction):**
  2H⁺ + 2e⁻ → H₂  (E° = 0.00 V)

### Proton Exchange Membrane (PEM)

Perfluorosulfonic acid (e.g., Nafion®) that:

* Conducts H⁺
* Insulates electrons
* Separates H₂ and O₂ gases

### Membrane Electrode Assembly (MEA)

Layered structure:

* Central PEM
* Catalyst layers (IrO₂/RuO₂ anode, Pt cathode)
* Gas diffusion layers (GDLs) with microporous sub-layers (MPL)

### Bipolar/Flow Field Plates

* Conduct current between cells
* Distribute reactant/product flows via channels
* Provide mechanical support and heat transfer
* Materials: coated steel, graphite, titanium

## Process Description I: System Layout & Core Unit

### System Boundaries

**Inputs:** Deionized water, DC electrical power
**Outputs:** H₂ gas, O₂ byproduct, waste heat, purge streams

**Sections:** Water treatment → Power conditioning → PEM stack → Gas conditioning → Cooling

### Simplified Process Flow Diagram (PFD)

See `docs/PFD.png` for a block diagram of streams and equipment.

### Feed Water Requirements

> Conductivity < 1 µS/cm (resistivity > 1 MΩ·cm) to protect PEM and catalysts.

### PEM Electrolyzer Stack

* **Cells per stack:** 40
* **Active area per cell:** 875 cm²
* Series electrical connection → U\_stack ≈ N\_cells × U\_cell

## Technical Calculations I: Stoichiometry & Production Rate

### Basis of Calculation

Use stack current (I\_stack) or current density (i\_c = I\_stack/A\_eff).

### Stoichiometry

* 1 mol H₂O → 1 mol H₂ + ½ mol O₂
* Water flow = 3–5× theoretical consumption (0.18–0.3 L/h range)

### Faraday’s Laws & Efficiency

```
η_f = (actual H₂ moles produced)/(theoretical moles from I )
```

Typical η\_f > 95%.

### Actual Production Rate

```
ṁ_H₂ (kg/s) = η_f · (I_stack / (2·F)) · M_H₂
```

## PEM Electrolysis Fundamentals II: Performance Factors

### Thermodynamics

* **Reversible voltage (E\_rev):** 1.23 V @ standard
* **Nernst correction** for T, P → E\_rev ≈ 1.5155 V @ 65 °C, 30 bar
* **Thermoneutral voltage (V\_tn):** \~1.48 V

### Kinetics & Overpotentials

```
U_cell = E_rev + η_act_anode + η_act_cathode + η_ohmic + η_conc
```

* Activation (catalyst-dependent)
* Ohmic (ionic/electronic resistance)
* Concentration (mass transport)

### Key Influencing Factors

* **Current density:** ↑ rate, ↑ U\_cell, ↓ η\_V
* **Temperature:** ↑ kinetics, ↑ conductivity
* **Pressure:** influences E\_rev and mass transport

## Technical Calculations II: Voltage, Energy & Efficiency

### Cell & Stack Voltage

Model at 65 °C, 30 bar:

```
U_cell(i) ≈ 1.5155 + 7.09·ln(7266·i/A_eff + 1) + 33.47·(i/A_eff)
```

U\_stack = 40·U\_cell

### Energy Consumption

```
P_DC = U_stack × I_stack
SEC (kWh/kg) = P_DC (kW)/ṁ_H₂ (kg/h)
```

### Efficiency Definitions

* **Voltage efficiency η\_V = E\_rev / U\_cell**
* **Stack efficiency η\_stack ≈ (V\_tn·η\_f)/U\_cell**

### Heat Generation

```
Q_gen = (U_stack - 40·V_tn) · I_stack
```

### Key Visualized Aspects

* Current & voltage vs. H₂ output curves
* Flow of water and gas streams
* Interactive parameters (i\_c, T, P)

### Assumptions & Simplifications

* Steady-state operation
* Ideal gas behavior
* Uniform cell conditions
* Simplified BOP models

## App Development

### Development Tools

* **Engine:** Unity 3D
* **Language/IDE:** C# with JetBrains Rider
* **3D Modeling:** Blender (+ BlenderKit, GrabCAD, JangaFX, FAB)
* **Scripting:** Python (visual simulations)

### Application Structure

1. **Main Menu**: Start, Options, Credits, Exit
2. **Production Plant**: Animated factory floor, process analysis overlay, voltage/current graph, water-flow video
3. **Molecular Level Analysis**: Exploded stack, animated molecule flow, adjustable current-density slider, live metrics

### Usage

1. Clone the repository.
2. Open `GreenH2Visualization.sln` in Rider.
3. Load the Unity project (`Assets/` folder).
4. Build and run on Windows platform.
5. Use keyboard/mouse to navigate scenes and overlays.

### Implementation Highlights

* **State Machine** drives visuals and interactions.
* **LineRenderer** + arrowheads for flow lines.
* **InfoTrigger** & **HoverInfo** scripts for contextual tooltips and highlights.
* **Object Pooler** for efficient molecule spawning and recycling.

## Conclusion & Future Work

### Summary of Contributions

Chemical engineering provided the electrochemical theory, process design, and quantitative models that underpin an accurate, interactive visualization.

### Significance & Challenges

Translating multiphysics and detailed models into real-time 3D required simplifying assumptions and close interdisciplinary coordination.

### Future Work Suggestions

* Dynamic modeling (start/stop, variable power)
* Degradation modeling (catalyst & membrane)
* Two-phase flow visualization
* Parameter exploration by users

## References

1. I. Staffell et al., "The role of hydrogen and fuel cells in the global energy system," *Energy & Environ. Sci.*, 2019.
2. M. Carmo et al., "A comprehensive review on PEM water electrolysis," *Int. J. Hydrogen Energy*, 2013.
3. X. Li et al., "PEM water electrolysis catalysts...," *Electrocatalysis*, 2021.
4. H. F. Araújo et al., "Proton-exchange membrane electrolysis for green H₂ production...\*, *Catalysts*, 2024.
5. G. Chisholm et al., "3D printed flow plates for water electrolysis...\*, *Energy & Environ. Sci.*, 2014.
6. M. Holst et al., "Cost forecast for low-temperature electrolysis...\*, Fraunhofer ISE, 2021.
7. O. Schmidt et al., "Future cost and performance of water electrolysis...\*, *Int. J. Hydrogen Energy*, 2017.
8. A. Ursúa et al., "Hydrogen production from water electrolysis...\*, *Proc. IEEE*, 2012.
9. G. Sakas et al., "Dynamic mass and energy balance model of a 50 kW PEM electrolyzer...\*, *Appl. Energy*, 2025.
10. F. Barbir, "PEM electrolysis for H₂ from renewables," *Solar Energy*, 2005.
