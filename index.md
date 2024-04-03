---
title: ORMIR-MIDS
subtitle: Bids
layout: default
---
# What it is
ORMIR-MIDS refer to two things:

* a standard specification for the processing of MR images of the human skeletal muscle, and
* a python package providing conversion and I/O functionalities for DICOM and ORMIR-MIDS data

The aim of this standard is to provide a common interface for data postprocessing and analysis tools to read and write data in an interoperable way. The existing DICOM standard has very broad guidelines that result in a large variability among vendors of medical devices, to the point that it can hardly be considered a "standard" at all.

The ORMIR-MIDS standard is inspired by the [neuroimaging BIDS specification](https://bids.neuroimaging.io/), and it is mostly compatible with it, in the sense that it aims to subdivide and group the acquired images based on their diagnostic role: e.g. anatomical images, quantitative maps, functional images, etc.

The images are stored as three- or four-dimensional [NIfTI](https://nifti.nimh.nih.gov/) datasets paired with three plain-text [JSON](https://www.json.org/) headers each. These images are stored in a predefined directory and naming structure that allows immediate identification of the role of each dataset.

As integration with medical and PACS systems is a prerequisites for our standard, bidirectional conversion between DICOM and ORMIR-MIDS is ensured.

ORMIR-MIDS is a fork and extension of [muscle-BIDS](https://github.com/muscle-bids/muscle-bids).

# The specification
ORMIR-MIDS prescribes that all imaging data should be kept in a NIfTI format inside a predefined directory structure, with a specific file naming scheme. Associated to each NIfTI file, there are up to three JSON files containing:

1. The relevant parameters for that specific acquisition (e.g. echo times for multi echo spin echo).
2. The patient information (which can be omitted for anonymization).
3. All extra headers needed for the conversion to DICOM (originating from the initial acquisition).

Each acquisition type has a corresponding set of relevant parameters and a naming convention. The full specification is found [here](/specs).

# The python package

A work-in-progress python package is delivered to implement the conversion between DICOM and ORMIR-MIDS, and the I/O of ORMIR-MIDS-compatible files from python programs. More information is found [here](/package).
