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
Where the `patient_folder` is the location of the root folder containing all the acquired data for a patient, divided into subfolders according to the MIDS extension of the BIDS standard, and as described below. The musculoskeletal tools will also output data in the correct format in the same folder structure. **NOTE: ** One important difference between ORMIR-MIDS and BIDS is that all MR-related outputs are prefixed by 'mr-' in ORMIR-MIDS (e.g. mr-anat, mr-quant, etc.). Please take this in to consideration when handling ORMIR-MIDS-derived data. 

# General guidelines

* Each ORMIR-MIDS dataset comprises:
    1. One NIfTI file containing the image data. This file is named `<patient>_<acquisition_type>.nii.gz`
    2. One JSON header named `<patient>_<acquisition_type>.json` (subsequently simply termed **header**) containing the imaging parameters relevant to the specific acquisition type.
    3. One JSON header named `<patient>_<acquisition_type>_patient.json` containing the patient information. This file can be omitted for anonymization purposes.
    4. One JSON header named `<patient>_<acquisition_type>_extra.json` containing a dictionary of DICOM fields used to convert the data back to DICOM.
* When it makes sense, 4D NIfTI datasets are used for imaging data instead of multiple 3D files (for example, multi-echo MRI data are stored as a fourth NIfTI dimension). The quantity that changes in the fourth dimension is identified by the parameter **`FourthDimension`** in the header. E.g. `"FourthDimension": "EchoTime"`. The value of the `FourthDimension` field must have a corresponding entry in the header, which is a list of values corresponding to each index along the fourth dimension. E.g. `"EchoTime": [3.9, 6.3]`.
* Multislice 2D imaging acquisitions are saved as a 3D NIfTI volume. To store the actual slice thickness, the **`AcquisitionVoxelSize`** parameter can be set in the header.
* Signal component suffixes for quantitative MRI:
    * Magnitude: No suffix
    * Phase (scaled -π/π): `_ph`
    * Real: `_real`
    * Imaginary: `_imag`
* **TODO:** Definition of multi-station data (e.g. whole-body acquisitions divided into multiple stacks). Proposal: add a `_stack` suffix to the filename.

# Guidelines for specific scan types

## Implemented or partially implemented

<table>
    <tr>
        <th><b>Imaging method/sequence</b></th>
        <th><b>NIfTI structure</b></th>
        <th><b>Filename suffix</b></th>
        <th><b>Folder</b></th>
        <th><b>JSON required fields</b></th>
    </tr>
    <tr>
        <td><b>Computed tomography</b></td>
        <td><b>3D (x,y,z)</b></td>
        <td><b>N/A</b></td>
        <td><b>ct</b></td>
        <td>
            <ul> 
                <li><b>XRayEnergy</b> in kVp</li>	
                <li><b>XRayExposure</b> in mAs</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Computed/ plain radiography</b></td>
        <td><b>2D (x,y)</b></td>
        <td><b>N/A</b></td>
        <td><b>cr</b></td>
        <td>
            <ul> 
                <li><b>ExposureTime</b> in ms</li>	
                <li><b>X-RayTubeCurrent</b> in mA</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>MRI: Multi-echo gradient echo</b></td>
        <td><b>4D (x,y,z,echo)</b></td>
        <td><b>megre</b></td>
        <td><b>mr-anat</b></td>
        <td>
            <ul> 
                <li><b>EchoTime</b> (array) in ms</li>	
                <li><b>WaterFatShift</b> in pixels</li>
                <li><b>MagneticFieldStrength</b></li>
                <li><i>[proposed]</i> <b>ReadoutMode</b>: Monopolar/Bipolar</li>
                <li><i>[proposed]</i> <b>PrecessionDirection</b>: Counter-/Clockwise</li> 
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>MRI: Multi-echo spin echo</b></td>
        <td><b>4D (x,y,z,echo)</b></td>
        <td><b>mese</b></td>
        <td><b>mr-anat</b></td>
        <td>
            <ul> 
                <li><b>EchoTime</b> (array) in ms</li>	
                <li><b>RefocusingFlipAngle</b> in degrees</li>
                <li><i>[optional]</i> <b>ExcitationProfile</b> and <b>RefocusingProfile</b>(arrays) providing the slice profiles in degrees</li> 
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>MRI: T1w / T1w-FS / T2w / T2w-FS</b></td>
        <td><b>3D (x,y,z)</b></td>
        <td><b>t1w / t1w-fs / t2w / t2w-fs</b></td>
        <td><b>mr-anat</b></td>
        <td>
        </td>
    </tr>
    <tr>
        <td><b>MRI: Quantitative T1 / T2 / wT2</b></td>
        <td><b>3D (x,y,z)</b></td>
        <td><b>t1 / t2 / wt2</b></td>
        <td><b>mr-quant</b></td>
        <td>
        </td>
    </tr>
</table>





## Not implemented / Proposed

<table>
    <tr>
        <th><b>Imaging method/sequence</b></th>
        <th><b>NIfTI structure</b></th>
        <th><b>Filename suffix</b></th>
        <th><b>Folder</b></th>
        <th><b>JSON required fields</b></th>
    </tr>
    <tr>
        <td><b>High-resolution peripheral quantitative computed tomography</b></td>
        <td><b>3D (x,y,z)</b></td>
        <td><b>N/A</b></td>
        <td><b>hrpqct</b></td>
        <td>
            <ul> 
                <li><b>XRayEnergy</b> in kVp</li>	
                <li><b>XRayExposure</b> in mAs</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>MRI: Phase contrast</b></td>
        <td><b>4D (x,y,z,t) + suffix per venc direction</b></td>
        <td><b>pc_mag / pc_ph_1 / pc_ph_2 / pc_ph_3</b></td>
        <td><b>mr-flow</b>?? The velocity information is stored as phase data scaled between -π and +π</td>
        <td>
            <ul> 
                <li><b>Venc</b> in cm/s</li>	
                <li><b>EncodingDirection</b> (3D vector) for each phase volume, indicating the direction of the positive velocity encoding for that volume. <b>TBD</b>: patient coordinate system or image coordinate system</li> 
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>MRI: DESS</b></td>
        <td><b>4D (x,y,z,echo)</b></td>
        <td><b>dess</b></td>
        <td><b>mr-anat</b></td>
        <td>
            <ul> 
                <li><b>EchoTime</b> (array) in ms</li>	
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>MRI: Diffusion</b></td>
        <td><b>4D (x,y,z,direction)</b></td>
        <td><b>diff</b></td>
        <td><b>mr-diff</b></td>
        <td>
            <ul> 
                <li><b>MixingTime</b> in ms</li>	
                <li><b>EncodingDirection</b> (array of 3D vectors). The norm of the vector is the <b>b-value</b>. The normalized vector indicates the <b>direction</b> of the diffusion gradient in patient coordinates</li> 
            </ul>
        </td>
    </tr>
    <tr>
        <td><b>Segmentation labels</b></td>
        <td>
            <ul>
                <li><b>3D (x,y,z)</b> with integer values, 0---N, each corresponding to a different label</li>
                <li><b>4D (x,y,z,label)</b> stack of binary (0/1) values, each dimension corresponding to a label</li>
            </ul>
        </td>
        <td><b>seg</b>??</td>
        <td><b>seg</b>??</td>
        <td>
            <ul>
                <li><b>Labels</b> (array of strings). List of the labels represented in the masks. The first value in the list corresponds to either a gray level of 0 or to the 1st volume in the fourth dimension. E.g. <i>["Background", "SOL", "VM", "VL"]</i></li>
                <li><b>Note</b>: the string representation of the labels must follow a standardized format. While it is possible that the same anatomical structure is represented by different labels (e.g. <i>SOL</i> or <i>Soleus</i>), the labels must be known. This allows flexibility in the implementation of segmentation tools, while keeping easy interoperability because all values are easily convertible. A list of standardized labels is visible <a href="https://docs.google.com/spreadsheets/d/e/2PACX-1vS4gioDvbO_6VItFglPEWeXP0U86tfG1yYifTU-XXqk5kdN1vln6KVP6bzDNPw-_L8xvkZ0soQeyW8-/pubhtml#">here</a>. Please contact <a href="mailto:francesco.santini@unibas.ch">Francesco Santini</a> if you would like to add your own definitions</li>
            </ul>
        </td>
    </tr>
</table>






