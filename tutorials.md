(tutorials)=
# 1. Converting DICOMs to the ORMIR-MIDS structure

The commandline script is called `dcm2omids.exe`. To view the commandline script help type
```commandline
dcm2omids -h
```

To use `ormir-mids` within Python, import the following modules
```python
from ormir_mids.utils.io import find_bids, load_bids
import nibabel as nib
```

For a detailed description of how to use `ormir-mids` see the following notebook
#### [ormir-mids usage: dcm2mbids](examples/jupyter/Muscle-bids_dcm2mbids.ipynb) [![Made withJupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange?style=for-the-badge&logo=Jupyter)](examples/jupyter/Muscle-bids_dcm2mbids.ipynb)

### 2. Exploring medical volumes with ORMIR-MIDS
`ormir-mids` can be used within Python to load, manipulate, and visualize medical volume datasets, without having to convert them to the ORMIR-MIDS structure.

- Load a DICOM file to a MedicalVolume object

```python
from ormir_mids.utils.io import load_dicom
```
```python
mv = load_dicom('<Path-to-DICOM-file>')
```

- Slice the volume. This will create a separate subvolume. Metadata will be sliced appropriately.
```python
mv_subvolume = mv[50:90, 50:90, 30:70]
```

- Convert volume to ITK image with [SimpleITK](https://simpleitk.org/)
```python
mv_itk = mv.to_sitk()
```

Examples of how to use `ormir-mids` for common data handling, image manipulation and processing tasks within Python can be found in this notebook
#### [ormir-mids usage: MedicalVolume class](examples/jupyter/Muscle-bids_MedicalVolume_tests.ipynb) [![Made withJupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange?style=for-the-badge&logo=Jupyter)](examples/jupyter/Muscle-bids_MedicalVolume_tests.ipynb)


<!-- In this page, you will get to know: 

1. [How to install and learn to use ORMIR-MIDS](installing)
2. [How ORMIR-MIDS works and how to contribute](how-it-works) -->

---
