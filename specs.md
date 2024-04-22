---
title: ORMIR-MIDS specification
subtitle: Version 0.1
layout: default
header-includes:
  - \newcommand{\sectionbreak}{\clearpage}
---

<!--
# Table of contents
{: .no_toc}

* TOC
{:toc}
-->

# Rationale
The goal of this standard is to have a uniform interface for software tools for musculoskeletal image processing and analysis.

Ideally, each tool will have a command-line interface with the following syntax:
```
musculoskeletal_tool <patient_folder>
```
Where the `patient_folder` is the location of the root folder containing all the acquired data for a patient, divided in subfolders according to the BIDS standard and as described below. The musculoskeletal tools will also output data in the correct format in the same folder structure.

# General guidelines

* Each ORMIR-MIDS dataset is composed of:
    1. One NIfTI file containing the image data. This file is named `<patient>_<acquisition_type>.nii.gz`
    2. One JSON header named `<patient>_<acquisition_type>.json` (subsequently simply termed **header**) containing the imaging parameters relevant to the specific acquisition type.
    3. One JSON header named `<patient>_<acquisition_type>_patient.json` containing the patient information. This file can be omitted for anonymization purposes.
    4. One JSON header named `<patient>_<acquisition_type>_extra.json` containing a dictionary of DICOM fields used to convert the data back to DICOM.
* When it makes sense, 4D NIfTI datasets are used instead of multiple 3D files (for example, multi-echo data are stored as a fourth NIfTI dimension). The quantity that changes in the fourth dimension is identified by the parameter **`FourthDimension`** in the header. E.g. `"FourthDimension": "EchoTime"`. The value of the `FourthDimension` field must have a corresponding entry in the header, which is a list of values corresponding to each index along the fourth dimension. E.g. `"EchoTime": [3.9, 6.3]`.
* Multislice 2D acquisitions are saved as a 3D NIfTI volume. To store the actual slice thickness, the **`AcquisitionVoxelSize`** parameter can be set in the header.
* Signal component suffixes:
    * Magnitude: No suffix
    * Phase (scaled -π/π): `_ph`
    * Real: `_real`
    * Imaginary: `_imag`
* **TODO:** Definition of multi-station data (e.g. whole-body acquisitions divided into multiple stacks). Proposal: add a `_stack` suffix to the filename.

# Guidelines for specific scan types

## Implemented or partially implemented


||NIfTI structure|Filename suffix|Folder|JSON required fields|
|---|---|---|---|---|
|**Multi-echo gradient echo**|**4D (x,y,z,echo)**|**megre**|**anat**|<ul> <li>**EchoTime** (array) in ms</li><li>**WaterFatShift** in pixels</li<li>**MagneticFieldStrength**</li><li>*[proposed]* **ReadoutMode**: Monopolar/Bipolar</li><li>*[proposed]* **PrecessionDirection**: Counter-/Clockwise</li> </ul>
|**Multi-echo spin echo**|**4D (x,y,z,echo)**|**mese**|**anat**|<ul><li>**EchoTime** (array) in ms</li><li>**RefocusingFlipAngle** in degrees</li><li>*[optional]* **ExcitationProfile** and **RefocusingProfile** (arrays) providing the slice profiles in degrees</li></ul>
|**T1w / T1w-FS / T2w / T2w-FS**|**3D (x,y,z)**|**t1w / t1w-fs / t2w / t2w-fs**|**anat**||
|**Quantitative T1 / T2 / wT2**|**3D (x,y,z)**|**t1 / t2 / wt2**|**quant**||


<!--

### Multi-echo gradient echo
* NIfTI structure: **4D (x,y,z,echo)**
* Filename suffix: **megre**
* Folder: **anat**
* JSON required fields:
    * **EchoTime** (array) in ms
    * **WaterFatShift** in pixels
    * **MagneticFieldStrength**
    * *[proposed]* **ReadoutMode**: Monopolar/Bipolar
    * *[proposed]* **PrecessionDirection**: Counter-/Clockwise

### Multi-echo spin echo

* NIfTI structure: **4D (x,y,z,echo)**
* Filename suffix: **mese**
* Folder: **anat**
* JSON required fields:
    * **EchoTime** (array) in ms
    * **RefocusingFlipAngle** in degrees
    * *[optional]* **ExcitationProfile** and **RefocusingProfile** (arrays) providing the slice profiles in degrees.

### T1w / T1w-FS / T2w / T2w-FS

* NIfTI structure: **3D (x,y,z)**
* Filename suffix: **t1w / t1w-fs / t2w / t2w-fs**
* Folder: **anat**

### Quantitative T1 / T2 / wT2

* NIfTI structure: **3D (x,y,z)**
* Filename suffix: **t1 / t2 / wt2**
* Folder: **quant**
-->

## Not implemented / Proposed
||NIfTI structure|Filename suffix|Folder|JSON required fields|
|---|---|---|---|---|
|**Phase contrast**|**4D (x,y,z,t) + multiple suffixes for venc direction**|**pc_mag / pc_ph_1 / pc_ph_2 / pc_ph_3**|**flow** ?? The velocity information is stored as phase data scaled between -π and +π|<ul><li>**Venc** in cm/s</li><li>**EncodingDirection** (3D vector) for each phase volume, indicating the direction of the positive velocity encoding for that volume. **TBD**: patient coordinate system or image coordinate system.</li></ul>|
|**Diffusion**|**4D (x,y,z,direction)**|**diff**|**diff**|<ul><li>**MixingTime** in ms</li><li>**EncodingDirection** (array of 3D vectors). The norm of the vector is the **b-value**. The normalized vector indicates the **direction** of the diffusion gradient in patient coordinates.</li></ul>|
|**Segmentation labels**|<ul><li>**3D (x,y,z)** with integer values, from 0 to N, each value corresponding to a different label</li><li>**4D (x,y,z,label)** stack of binary (0/1) values, each dimension corresponding to a label</li><ul>|**seg** ??|**seg** ??|<ul><li>**Labels** (array of strings). List of the labels represented in the masks. The first value in the list corresponds to either a gray level of 0 or to the 1st volume in the fourth dimension. E.g. `["Background", "SOL", "VM", "VL"]`</li></li>**Note**: the string representation of the labels must follow a standardized format. While it is possible that the same anatomical structure is represented by different labels (e.g. `SOL` or `Soleus`), the labels must be known. This allows flexibility in the implementation of segmentation tools, while keeping easy interoperability because all values are easily convertible. A list of standardized labels is visible [here](https://docs.google.com/spreadsheets/d/e/2PACX-1vS4gioDvbO_6VItFglPEWeXP0U86tfG1yYifTU-XXqk5kdN1vln6KVP6bzDNPw-_L8xvkZ0soQeyW8-/pubhtml#). Please contact [Francesco Santini](mailto:francesco.santini@unibas.ch) if you would like to add your own definitions.</li></ul>


<!--
### Phase contrast

* NIfTI structure: **4D (x,y,z,t) + multiple suffixes for venc direction**
* Filename suffix: **pc_mag / pc_ph_1 / pc_ph_2 / pc_ph_3**
* Folder: **flow** ??
* The velocity information is stored as phase data scaled between -π and +π.
* JSON required fields:
    * **Venc** in cm/s
    * **EncodingDirection** (3D vector) for each phase volume, indicating the direction of the positive velocity encoding for that volume. **TBD**: patient coordinate system or image coordinate system.

### Diffusion

* NIfTI structure: **4D (x,y,z,direction)**
* Filename suffix: **diff**
* Folder: **diff** ??
* JSON required fields:
    * **MixingTime** in ms
    * **EncodingDirection** (array of 3D vectors). The norm of the vector is the **b-value**. The normalized vector indicates the **direction** of the diffusion gradient in patient coordinates.

### Segmentation labels

* NIfTI structure: 
    * **3D (x,y,z)** with integer values, from 0 to N, each value corresponding to a different label
    * **4D (x,y,z,label)** stack of binary (0/1) values, each dimension corresponding to a label
* Filename suffix: **seg** ??
* Folder: **seg** ??
* JSON required fields:
    * **Labels** (array of strings). List of the labels represented in the masks. The first value in the list corresponds to either a gray level of 0 or to the 1st volume in the fourth dimension. E.g. `["Background", "SOL", "VM", "VL"]`
    * **Note**: the string representation of the labels must follow a standardized format. While it is possible that the same anatomical structure is represented by different labels (e.g. `SOL` or `Soleus`), the labels must be known. This allows flexibility in the implementation of segmentation tools, while keeping easy interoperability because all values are easily convertible. A list of standardized labels is visible [here](https://docs.google.com/spreadsheets/d/e/2PACX-1vS4gioDvbO_6VItFglPEWeXP0U86tfG1yYifTU-XXqk5kdN1vln6KVP6bzDNPw-_L8xvkZ0soQeyW8-/pubhtml#). Please contact [Francesco Santini](mailto:francesco.santini@unibas.ch) if you would like to add your own definitions.
-->