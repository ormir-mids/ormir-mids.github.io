(specs)=
# ORMIR-MIDS as a Standard Specification

The ORMIR-MIDS specifications are a simple and intuitive way to organize MSK imaging data. They are an extension of the specifications of the Brain Imaging Data Structure ([BIDS](https://bids.neuroimaging.io/index.html)) and the Medical Imaging Data Structure ([MIDS](https://arxiv.org/abs/2010.00434))

In this page, you will find:   
{ref}`1. Structure and naming of folders and files<structure-naming>`  
{ref}`2. Supported imaging modalities<supported-modalities>`  
{ref}`3. Current and future work<current-future-work>`

---


(structure-naming)=
## Structure and naming of folders and files

(folder-structure)=
### Folder structure  

The folder structure is hierarchical and composed of 4 levels of nested folders:  
*Dataset* &rarr; *Subject* &rarr; *Session* &rarr; *Imaging Method*

```{figure} ./figures/folder_structure.png
:label: folderStructure
:alt: ORMIR-MIDS folder structure
:height: 200px
:align: center
```

- *Dataset*:  **root (or parent) folder** containing all the MSK data (E.g., `Dataset_organized`)
- *Subject*: folder(s) containing all the **data about a single subject** (E.g., `sub-01` for the first subject)
- *Session*: folder(s) containing the data of an acquisition session **at a specific time point**(E.g., `ses-01` for baseline acquisitions)
- *Imaging Method*: folder(s) containing the **data of a specific acquisition**. (E.g., `mr-anat` for anatomical MR images). You can find the  currently supported imaging methods in {ref}`this table <supported-modalities>`  


---


### Filesystem structure

Within each folder or subfolder, there are specific files:

```{figure} ./figures/filesystem_structure.png
:label: filesystemStructure
:alt: ORMIR-MIDS file system structure
:height: 200px
:align: center
```
- *Participants' information*: definition under construction!
- *Scans' information*: definition under construction!
- *Session information*: definition under construction!
- *Image volume*: **3D image** 
- *Image information*: **Header** of the dicom images in `.json` format


---


(naming)=
### Folder naming
- Folders have precise names:
```{figure} ./figures/folder_nomenclature.png
:label: folderNomenclature
:alt: ORMIR-MIDS folder nomenclature
:height: 230px
:align: center
```
- Folder names referring to *subjects and sessions* are composed of two parts:
  1. `sub` or `ses`, indicating *subject* (blue in the figure above) or *session* (purple in the figure above) 
  2. `<ID>` of the *subject* or of the *session* (e.g., `01`)   
  
  *Note*: The two parts are separated by dash (`-`)

- Folder names referring to *image modalities* (yellow in the figure above) can have various names, such as `mr-anat`, `ct`, etc. For a list of the available names, see the second column (called *Folder name*) in {ref}`the table below<supported-modalities>`    

 
---


(file-naming)=
### File naming
- Files have precise names:
```{figure} ./figures/file_nomenclature.png
:label: fileNomenclature
:alt: ORMIR-MIDS file nomenclature
:height: 230px
:align: center
```
- Each file name is composed of three parts, each of them containing information about:
  1. *Subject*, such as `sub-01` (blue in the figure above)
  2. *Session*, such as `ses-01` (purple in the figure above)
  3. *File content*, such as `scans`, `metadata`, etc. (green in the figure above). For the images, you can find the  currently supported file types in {ref}`the table below<supported-modalities>`      

  *Note*: The three parts are separated by underscore (`_`)


---


(supported-modalities)=
## General JSON Fields

The JSON fields in the following table are common to all acquisition types of a specific modality. Refer to the section below for specific acquisition types within a modality.
The table columns specify:  
- *Imaging method*: the image acquisition method, such as `computed tomography`, `MR imaging`, etc.
- *Folder names*: name of the output folder containing the images (e.g., `mr-anat`, `ct`, etc.). See the {ref}`folder naming specifications <folder-structure>` for more details
- *File name suffix*: suffix of the file name of the image volume (e.g., `mese`, `megre`, etc.). See the {ref}`file naming specifications <file-naming>` for more details
- *Image volume*: dimension (`2D`, `3D`, or `4D`) and directions (`x`, `y`, `z`, `echo`) of the obtained image volume (i.e., `nii.gz` files)
- *JSON fields*: information that the dicom header must have to be able to transform the data into the ORMIR-MIDS structure. Fields in **bold** are mandatory. Units (if available) are in square brackets.


```{list-table}
:header-rows: 1

* - Imaging method
  - Folder name(s)
  - File name suffix
  - Image volume
  - JSON fields
* - Computed tomography
  - ct
  - N/A
  - 3D (x,y,z)
  - **XRayEnergy** [kVp]
    <br> **XRayExposure** [mAs]
* - Computed / plain radiography
  - cr
  - N/A
  - 2D (x,y)
  - **ExposureTime** [ms]
    <br> **X-RayTubeCurrent** [mA]
* - MRI
  - mr-anat/mr-quant
  - [various]
  - 3D, 4D, or 5D
  - **EchoTime** [ms]<br/>
  **RepetitionTime** [ms]<br/>
  **FlipAngle** [degrees]<br/>
  RefocusingFlipAngle [degrees]<br/>
  InversionTime [ms]<br/>
  ScanningSequence<br/>
  SequenceVariant<br/>
  ScanOptions<br/>
  SequenceName<br/>
  MRAcquisitionType<br/>
  ParallelReductionFactorInPlane<br/>
  ParallelAcquisitionTechnique<br/>
  PartialFourier<br/>
  PartialFourierDirection<br/>
  PixelBandwidth [Hz/px]<br/>
  Manufacturer<br/>
  ImagingFrequency [MHz]<br/>
  MagneticFieldStrength [T]<br/>
  ImageType<br/>
  PhaseEncodingDirection<br/>
* - MRI: T1w / T1w-FS / T2w / T2w-FS
  - mr-anat
  - t1w / t1w-fs / t2w / t2w-fs
  - 3D (x,y,z)
  - 
* - MRI: Quantitative T1 / T2 / wT2
  - mr-quant
  - t1 / t2 / wt2
  - 3D (x,y,z)
  - 
```


---

(acquisition-specs-section)=
## Acquisition-specific specifications


```{toctree}
:glob:
:titlesonly:

specs/*
```


---


(current-future-work)=
## Current and future work


We are working on converters for:
- More imaging modalities, such as HR-pQCT, MRI Diffusion  
- Derived data, such as segmentation labels

Here are the specs of some imaging modalities we will support:

**Diffusion**

* NIfTI structure: **4D (x,y,z,direction)**
* Filename suffix: **diff**
* Folder: **diff** ??
* JSON required fields:
    * **MixingTime** in ms
    * **EncodingDirection** (array of 3D vectors). The norm of the vector is the **b-value**. The normalized vector indicates the **direction** of the diffusion gradient in patient coordinates.

**Segmentation labels**

* NIfTI structure: 
    * **3D (x,y,z)** with integer values, from 0 to N, each value corresponding to a different label
    * **4D (x,y,z,label)** stack of binary (0/1) values, each dimension corresponding to a label (one-hot encoding)
* Filename suffix: **seg** ??
* Folder: **seg** ??
* JSON required fields:
    * **Labels** (array of strings). List of the labels represented in the masks. The first value in the list corresponds to either a gray level of 0 or to the 1st volume in the fourth dimension. E.g. `["Background", "SOL", "VM", "VL"]`
    * **Note**: the string representation of the labels must follow a standardized format. While it is possible that the same anatomical structure is represented by different labels (e.g. `SOL` or `Soleus`), the labels must be known. This allows flexibility in the implementation of segmentation tools, while keeping easy interoperability because all values are easily convertible. A list of standardized labels is visible [here](https://docs.google.com/spreadsheets/d/e/2PACX-1vS4gioDvbO_6VItFglPEWeXP0U86tfG1yYifTU-XXqk5kdN1vln6KVP6bzDNPw-_L8xvkZ0soQeyW8-/pubhtml#). Please contact [Francesco Santini](mailto:francesco.santini@unibas.ch) if you would like to add your own definitions.


---
