# (MR) Velocity quantification [Draft]

```{list-table}
:header-rows: 1

* - Imaging method
  - Folder name
  - File name suffix
  - Image volume
  - JSON fields
* - MRI: Velocity quantification
  - mr-quant
  - vel
  - 5D (x,y,z,t,direction)
  - FourthDimension: "TriggerTime"<br/>
  TriggerTime [array, ms]<br/>
  FifthDimension: "VelocityEncodingDirection"<br/>
  VelocityEncodingDirection [array, vectors]<br/>
  Venc [array, m/s]
```

## Notes
1. The actual velocity in **m/s** is stored in the volume data. The range of the values is from *-Venc* to *+Venc* for every encoding direction.

2. The VelocityEncodingDirection field is an array of vectors that identify which velocity direction is encoded in the corresponding dimension of the volume. The following example corresponds to three directional encoding, the first of which is along the row direction (*x*), the second along the column direction (*y*), and the third along the slice direction (*z*):
```
[[1,0,0],[0,1,0],[0,0,1]]
```

3. The Venc is an array that provides the original Venc for every dimension of the volume. This is only included for velocity-to-noise-ratio considerations, but not necessary for the interpretation of the data, which is already scaled appropriately.
