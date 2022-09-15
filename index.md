---
title: Muscle-BIDS
subtitle: Bids
layout: default
---
# What it is
Muscle-BIDS refer to two things:

* a standard specification for the processing of MR images of the human skeletal muscle, and
* a python package providing conversion and I/O functionalities for DICOM and muscle-BIDS data

The aim of this standard is to provide a common interface for data postprocessing and analysis tools to read and write data in an interoperable way. The existing DICOM standard has very borad guidelines that result in a large variability among vendors of medical devices, to the point that it can hardly be considered a "standard" at all.

The muscle-BIDS standard is inspired by the [neuroimaging BIDS specification](https://bids.neuroimaging.io/), and it is mostly compatible with it, in the sense that it aims to subdivide and group the acquired images based on their diagnostic role: e.g. anatomical images, quantitative maps, functional images, etc.

The images are stored as three- or four-dimensional [NIfTI](https://nifti.nimh.nih.gov/) datasets paired with three plain-text [JSON](https://www.json.org/) headers each. These images are stored in a predefined directory and naming structure that allows immediate identification of the role of each dataset.

As integration with medical and PACS systems is a prerequisites for our standard, bidirectional convertion between DICOM and muscle-BIDS is ensured.

# Who we are
The Muscle-BIDS draft was based on the [neuroimaging BIDS specification](https://bids.neuroimaging.io/) by the following consortium of MR researchers:

* Francesco Santini (University of Basel, Switzerland)
* Martijn Froeling (UMC Utrecht, the Netherlands)
* Hermien Kan and Donnie Cameron (UMC Leiden, the Netherlands)
* David Bendahan and Amira Trabelsi (Aix-Marseille University, France)
* John Torton and Kanber Baris (University College London, UK)
* Dimitrios Karampinos and Sarah Schlaeger (Technical University Munich, Germany)
* Arjun Desai (Stanford University, USA)

Additionally, the muscle-bids python [package](https://pypi.org/project/muscle-bids/) is developed by:

* Francesco Santini
* Donnie Cameron
* Leonardo Barzaghi
* Judith Cueto Fernandez
* Jilmen Quintiens

# The specification

