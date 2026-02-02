# (MR) Multi-echo spin echo

```{list-table}
:header-rows: 1

* - Imaging method
  - Folder name
  - File name suffix
  - Image volume
  - JSON fields
* - MRI: Multi-echo spin echo
  - mr-anat
  - mese
  - 4D (x,y,z,echo)
  - EchoTime (array) in ms <br>	
    RefocusingFlipAngle in degrees<br>
    *optional:* ExcitationProfile and RefocusingProfile (arrays) providing the slice profiles in degrees
```
