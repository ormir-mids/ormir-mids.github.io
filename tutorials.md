(tutorials)=
# Tutorials
### 1. Converting DICOMs to the ORMIR-MIDS structure

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
#### [ormir-mids usage: dcm2omids](https://mybinder.org/v2/gh/ormir-mids/ormir-mids/HEAD?urlpath=%2Fdoc%2Ftree%2Fjupyter%2Formir-mids-dcm2omids.ipynb) [![Made withJupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange?style=for-the-badge&logo=Jupyter)](https://mybinder.org/v2/gh/ormir-mids/ormir-mids/HEAD?urlpath=%2Fdoc%2Ftree%2Fjupyter%2Formir-mids-dcm2omids.ipynb)
