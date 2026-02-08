(documentation)=
# Documentation and Tutorials
# Command-line conversion tool

The commandline script is called `dcm2omids.exe`. To view the commandline script help type
```commandline
dcm2omids -h

usage: dcm2omids [-h] [--anonymize [pseudo_name]] [--recursive] [--series-number] [--disable-patient-json] [--disable-extra-json] [--session session_id] input_folder output_folder

Convert DICOM to ORMIR-MIDS format

positional arguments:
  input_folder          Input folder
  output_folder         Output folder

options:
  -h, --help            show this help message and exit
  --anonymize [pseudo_name], -a [pseudo_name]
                        Use the pseudo_name (default: anon) as patient name
  --recursive, -r       Recurse into subfolders
  --series-number, -s   Add series number to file name
  --disable-patient-json, -p
                        Avoid saving patient json file
  --disable-extra-json, -e
                        Avoid saving extra json file
  --session session_id  Specify the session ID to use (default: none)

```

# Using the `series_config.json` companion file
The optional companion file `series_config.json` can define overrides and multiseries config sections to control conversion behavior. This file **must be placed in the same base folder passed to dcm2omids for conversion**.

The multiseries config is necessary when the same dataset is spread across multiple series, for example when each echo of a multi-echo gradient-echo sequence has its own series (as it happens with Siemens).

Overrides are defined in the same file using the special key "overrides" key inside the JSON object, and they are needed when a specific value in the ormir-mids header needs to be forced.

## List expressions
List expressions can be used both for overrides and for multiseries configuration, to specify a list of series in a compact way. As an alternative, the series numbers can also be listed explicitly as a list of integers.
- List expression format: `[<start>:<step>:<end>] or [<start>:<step>:n<count>]`
  - Integers: [1:2:11] or [1:2:n3] (Note: the step must always be defined!)
  - Floats: [0.5:0.5:2.0] or [0.5:0.5:n4]
- The list expression must be saved as a string in the JSON (enclosed in double quotes)


## Overrides
Use overrides to set or replace OMIDS header values for specific series.
### Syntax
- overrides is an object where keys are series numbers or list expressions.
- Values are objects of header keys and override values. 
- When a list is used as an override value and its length matches the series list length, each series receives its corresponding value.

## Multiseries configuration
Use multiseries config to group multiple series into a single concatenated 4D volume.
### Syntax
- The top-level object contains group names and their series lists.
- Each group value is either:
  - A list of series numbers or relative paths, or
  - A list expression.
- Series numbers are compared with DICOM tag 0020,0011.
- Paths are resolved relative to the input folder and compared using absolute paths.

### Notes
- When all series in a group are present, volumes are concatenated and saved as a single file.
- The group name is only used for tracking; output naming follows the converter’s rules.

## Example
```python
{
  "overrides": {
     "3": {
       "Modality": "MR"
     }, 
     "[10:1:12]": {
       "EchoTime": "[10:5:n3]"
     }
  },
  "T1_group": [1,2,3],
  "fMRI_group": "[4:1:8]", 
  "local_paths_group": ["subdir/seriesA", "subdir/seriesB"]
}
```

To use `ormir-mids` within Python, import the following modules
```python
from ormir_mids.utils.io import find_bids, load_bids
import nibabel as nib
```

# Notebook tutorial
For a detailed description of how to use `ormir-mids` see the following notebook
#### [ormir-mids usage: dcm2omids](https://mybinder.org/v2/gh/ormir-mids/ormir-mids/HEAD?urlpath=%2Fdoc%2Ftree%2Fjupyter%2Formir-mids-dcm2omids.ipynb) [![Made withJupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange?style=for-the-badge&logo=Jupyter)](https://mybinder.org/v2/gh/ormir-mids/ormir-mids/HEAD?urlpath=%2Fdoc%2Ftree%2Fjupyter%2Formir-mids-dcm2omids.ipynb)