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

Additionally, the muscle-bids python [package](/package) is developed by:

* Francesco Santini
* Donnie Cameron
* Leonardo Barzaghi
* Judith Cueto Fernandez
* Jilmen Quintiens

# The specification

Muscle-BIDS prescribes that all imaging data should be kept in a NIfTI format inside a predefined directory structure, with a specific file naming scheme. Associated to each NIfTI file, there are up to three JSON files containing:

1. The relevant parameters for that specific acquisition (e.g. echo times for multi echo spin echo).
2. The patient information (which can be omitted for anonymization).
3. All extra headers needed for the conversion to DICOM (originating from the initial acquisition).

Each acquisition type has a corresponding set of relevant parameters and a naming convention. The full specification is found [here](/specs).

# The python package

A work-in-progress python package is delivered to implement the conversion between DICOM and Muscle-BIDS, and the I/O of Muscle-BIDS-compatible files from python programs. More information is found [here](/package).
