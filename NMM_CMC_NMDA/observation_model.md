## Function dissection `spm_dcm_erp_dipfit`

Function which prepares structures for ECD forward model.

- Get data filename and good channels
- Get source locations if MEG or EEG
- Fill in dipfit
    - DCM.M.dipfit.vol: gets its corresponding head model
    - DCM.M.dipfit.datareg: 
```matlab
  struct with fields:

     sensors: [1×1 struct]
     fid_eeg: [1×1 struct]
     fid_mri: [1×1 struct]
       toMNI: [4×4 double]
     fromMNI: [4×4 double]
    modality: 'EEG'
```
    - DCM.M.dipfit.sens

```matlab
  struct with fields:

     chanpos: [21×3 double]
     elecpos: [21×3 double]
    chantype: {1×21 cell}
    chanunit: {1×21 cell}
       label: {1×21 cell}
        unit: 'mm'
```

### Imaging (distributed source reconstruction)
- Load Gain or Lead field matrix
- Sets parameters:
	- defaults: Nm = 6; number of modes per region and rad=16
#187: do not understand the number of modes per region stuff!
- Compute spatial basis (eigenmodes of lead field)

#214: Nm, by default 6 is being used for SVD! But didn't we want 7 here??

## Function dissection `spm_dcm_eeg_channelmodes`
Returns the channel eigenmodes.

number of modes required (upper bound) is an upper bound??

And here Nm is 7??

What is this "re-scale spatial projector"??