# (MR) Multi-echo gradient echo

```{list-table}
:header-rows: 1

* - Imaging method
  - Folder name
  - File name suffix
  - Image volume
  - JSON fields
* - MRI: Multi-echo gradient echo
  - mr-anat
  - megre
  - 4D (x,y,z,echo)
  - EchoTime (array) in ms 
    <br> WaterFatShift in pixels 
    <br> MagneticFieldStrength 
    <br> *proposed:* ReadoutMode: Monopolar/Bipolar 
    <br> *proposed:* PrecessionDirection: Counter-/Clockwise
```
