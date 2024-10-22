(specs)=
# ORMIR-MIDS as a Standard Specification

The ORMIR-MIDS specifications are a simple and intuitive way to organize MSK imaging data. They are an extension of the specifications of the Brain Imaging Data Structure ([BIDS](https://bids.neuroimaging.io/index.html)) and the Medical Imaging Data Structure ([MIDS](https://arxiv.org/abs/2010.00434))

In this page, you will find:   
{ref}`1. Structure and naming of folders and files<structure-naming>`  
{ref}`2. Supported imaging modalities<supported-modalities>`  


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
## Supported imaging modalities


In the following table, you will find the image data types that are currently implemented or under development in ORMIR-MIDS. The table columns specify:  
- *Imaging method*: the image acquisition method, such as `computed tomography`, `MR imaging`, etc.
- *Folder name*: name of the output folder containing the images (e.g., `mr-anat`, `ct`, etc.). See the {ref}`folder naming specifications <folder-structure>` for more details
- *File name suffix*: suffix of the file name of the image volume (e.g., `mese`, `megre`, etc.). See the {ref}`file naming specifications <file-naming>` for more details
- *Image volume*: dimension (`2D`, `3D`, or `4D`) and directions (`x`, `y`, `z`, `echo`) of the obtained image volume (i.e., `nii.gz` files)
- *JSON fields*: information that the dicom header must have to be able to transform the data into the ORMIR-MIDS structure

```{list-table}
:header-rows: 1

* - Imaging method
  - Folder name
  - File name suffix
  - Image volume
  - JSON fields
* - Computed tomography
  - ct
  - N/A
  - 3D (x,y,z)
  - XRayEnergy in kVp 
    <br> XRayExposure in mAs
* - Computed / plain radiography
  - cr
  - N/A
  - 2D (x,y)
  - ExposureTime in ms 
    <br> X-RayTubeCurrent in mA
* - MRI: Multi-echo gradient echo
  - mr-anat
  - megre
  - 4D (x,y,z,echo)
  - EchoTime (array) in ms 
    <br> WaterFatShift in pixels 
    <br> MagneticFieldStrength 
    <br> *proposed:* ReadoutMode: Monopolar/Bipolar 
    <br> *proposed:* PrecessionDirection: Counter-/Clockwise
* - MRI: Multi-echo spin echo
  - mr-anat
  - mese
  - 4D (x,y,z,echo)
  - EchoTime (array) in ms <br>	
    RefocusingFlipAngle in degrees<br>
    *optional:* ExcitationProfile and RefocusingProfile (arrays) providing the slice profiles in degrees
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

*Note*: We are also working on conversions for:
- More imaging modalities, such as HR-pQCT, MRI Phase contrast, MRI DESS, MRI Diffusion  
- Derived data, such as segmentation labels

---



https://github.com/ormir-mids/ormir-mids.github.io/issues/new?title=Issue%20on%20page%20%2Fpackage.html&body=Your%20issue%20content%20here.
https://github.com/ORMIRcommunity/ormir_index_guidelines/issues/new?title=Issue%20on%20page%20%2Findex.html&body=Your%20issue%20content%20here.