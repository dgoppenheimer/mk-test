---
title: "Course Organization"
date: 2022-02-08
description: >
  This article gives a brief description of how the course, *Practical Molecular Dynamics*, is organized.
---

## Introduction

### Learning Objectives

## Course Summary

| Part   | Lab    | Topic                                | Date |
| ------ | ------ | ------------------------------------ | ---- |
| Part 1 |        | **Getting Started**                  |      |
|        | Lab 01 | Introduction to  <br/>Jupyter, Colab |      |
|        | Lab 03 | analyzing PDB files                  |      |
|        | Lab 04 | NGLView                              |      |
|        | Lab 05 | PyMOL                                |      |
| Part 2 |        | **MD Simulations**                   |      |
|        | Lab 06 | Introduction                         |      |
|        | Lab 07 | protein simulations                  |      |
|        | Lab 08 | ligand-protein simulations           |      |
| Part 3 |        | **Analysis of Trajectories**         |      |
|        | Lab 09 | Introduction                         |      |
|        | Lab 10 | MDAnalysis <br/>and correlationplus  |      |
|        | Lab 11 | MD-Task and `gmx`                    |      |

## Course Outline

- Part 1. Getting Started
    - introduction to Jupyter on Colab
    - working with PDB files
        - PDBFixer
        - grep, awk, VSCode
    - viewing protein structures
        - NGLView
        - PyMOL
        - VMD
        - Chimera/ChimeraX (optional) --probably delete this

- Part 2. Molecular Dynamics Simulations
    - introduction
        - simulation programs
            - OpenMM
            - GROMACS
            - Acellera ACEMD
            - AMBER (optional)
            - NAMD (optional)
        - force fields
            - AMBER
            - CHARMM
            - OpenFF
            - CGenFF
            - GAFF2
    - simulations
        - protein simulations
        - ligand-protein simulations
            - docking (Vina/Smina, Dock, MTiOpenScreen)
        - membrane protein simulations (optional)

- Part 3. Analysis of Trajectories
    - introduction
    - software tools
        - MDAnalysis- correlationplus
        - GROMACS
        - MD-Task (may not work on colab)
        - MDTraj
        - Bio3D (optional)

    - analyses
        - RMSD, RMSF
        - Ramachandran plot
        - principle component analysis (PCA)
        - residue interaction network (RIN) analysis
        - perturbation response scanning (PRS)
        - dynamic cross-correlation (MD-Task) (may not work on colab)

## Additional Resources

See this course from the summer of 2021, [CHEM 181 Introduction to Molecular Simulation](http://copresearch.pacific.edu/mmccallum/181/index.html).

[CHEM 181 Syllabus](http://copresearch.pacific.edu/mmccallum/181/resources/New-Syllabus.pdf)

The course is set up for 5 weeks.

[bash tutorial](http://www.hypexr.org/bash_tutorial.php#tips)  
[PDBFixer](https://htmlpreview.github.io/?https://github.com/openmm/pdbfixer/blob/master/Manual.html)

### Getting Started Resources

#### The Command Line and Shells

#### Text Editors

- [VS Code](https://code.visualstudio.com/)
- [VS Code on the web](https://vscode.dev/)

- [BBEdit](https://www.barebones.com/products/bbedit/)

#### Graphing with Plotly

- [Plotly Fundamentals](https://plotly.com/python/plotly-fundamentals/)
- [Plotly Tutorials](https://www.geeksforgeeks.org/python-plotly-tutorial/)
- [Jupyter Notebook Tutorial in Python](https://plotly.com/python/ipython-notebook-tutorial/)

## Questions About Protein Structure Validation

See [Structure validation practical - answers](https://www.ebi.ac.uk/pdbe/modval-answers)

## Other Courses

[Molecular Dynamics simulations in Python](https://klyshko.github.io/teaching/2019-03-01-teaching)
