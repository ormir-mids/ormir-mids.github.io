# (MR) MR Strain mapping [Draft]

```{list-table}
:header-rows: 1

* - Imaging method
  - Folder name
  - File name suffix
  - Image volume
  - JSON fields
* - MRI: Strain Eigenvalues
  - mr-quant
  - strain
  - 5D (x,y,z,t,ev_order)
  - FourthDimension: "TriggerTime"<br/>
  TriggerTime [array, ms]<br/>
  FifthDimension: "EigenOrder"
* - MRI: Strain Eigenvectors
  - mr-quant
  - strain-vec
  - 6D (x,y,z,t,ev_order,vector_component)
  - FourthDimension: "TriggerTime"<br/>
  TriggerTime [array, ms]<br/>
  FifthDimension: "EigenOrder"<br/>
  SixthDimension: "VectorComponent"
* - MRI: Strain Rate Eigenvalues
  - mr-quant
  - strain-rate
  - 5D (x,y,z,t,ev_order)
  - FourthDimension: "TriggerTime"<br/>
  TriggerTime [array, ms]<br/>
  FifthDimension: "EigenOrder"
* - MRI: Strain Rate Eigenvectors
  - mr-quant
  - strain-rate-vec
  - 6D (x,y,z,t,ev_order,vector_component)
  - FourthDimension: "TriggerTime"<br/>
  TriggerTime [array, ms]<br/>
  FifthDimension: "EigenOrder"<br/>
  SixthDimension: "VectorComponent"
```

## Notes
1. The EigenOrder (indicated as `ev_order` in the dimensions description above) corresponds to the following:
   - First Eigenvalue/Eigenvector: Largest positive Eigenvalue.
   - Second Eigenvalue/Eigenvector: Largest negative Eigenvalue.
   - Third Eigenvalue/Eigenvector: Remaining Eigenvalue.
2. The vector components are expressed in the same reference system as the volume.
