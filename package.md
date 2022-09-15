---
title: muscle-bids python package
layout: default
---

In order to aid the conversion and the implementation of the muscle-BIDS standard, we are working on a python package that can perform the identification of the correct scan types from DICOM datasets and appropriately convert them. Additionally, the package provides functions for the I/O of muscle-BIDS datasets in python programs, providing functions to identify the desired scan type, read header fields, etc.

The package was partly developed thanks to the support of the [ORMIR](https://ormircommunity.github.io/) (formerly JC\|MSK) community during the Maastricht 2022 workshop and hackaton “Building the Jupyter Community in Musculoskeletal Imaging Research” and is part of its core projects.

# Python resources
* The muscle-bids package can be installed by: `pip install muscle-bids`
* The package source is available at [https://github.com/muscle-bids/muscle-bids](https://github.com/muscle-bids/muscle-bids)
* An interactive tutorial on its usage is available through Google Colab [here](https://colab.research.google.com/github/muscle-bids/muscle-bids/blob/main/jupyter/Muscle-bids_dcm2mbids.ipynb).