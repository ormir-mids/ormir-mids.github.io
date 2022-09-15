---
title: Muscle-BIDS specification
subtitle: Version 0.1
layout: default
header-includes:
  - \newcommand{\sectionbreak}{\clearpage}
---

# Rationale
The goal of this standard is to have a uniform interface for software tools for muscle imaging.

Ideally, each tool will have a command-line interface with the following syntax:
```
muscle_tool <patient_folder>
```
Where the `patient_folder` is the location of the root folder containing all the acquired data for a patient, divided in subfolders according to the BIDS standard and as described below. The muscle tools will also output data in the correct format in the same folder structure.

# General guidelines

* Each Muscle-BIDS (following: **mBIDS**) dataset is composed of:
* 1. One NIfTI file containing the image data. This file is named `<patient>_<acquisition_type>.nii.gz`
* 2. One JSON header named `<patient>_<acquisition_type>.json` containing the imaging parameters relevant to the specific acquisition type.
* 3. 

* When it makes sense, 4D NIfTI datasets are used instead of multiple 3D files (for example, multi-echo data are stored as a fourth NIfTI dimension). The quantity that changes in the fourth dimension is identified by 