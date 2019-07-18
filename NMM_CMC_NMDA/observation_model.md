## Function dissection `spm_dcm_erp_dipfit`

Function which prepares structures for ECD forward model. Defines spatial model?

```
% needs:
%       DCM.xY.Dfile 			% <path/to/preprocessed/EEG/data>
%       DCM.xY.Ic				% Good channel indices
%       DCM.Lpos				% Position of sources
%       DCM.options.spatial     - 'ERP', 'LFP' or 'IMG'
%
% fills in:
%
%       DCM.M.dipfit
%
%    dipfit.location - 0 or 1 for source location priors
%    dipfit.symmetry - 0 or 1 for symmetry constraints on sources
%    dipfit.modality - 'EEG', 'MEG', 'MEGPLANAR' or 'LFP'
%    dipfit.type     - 'ECD', 'LFP' or 'IMG''
%    dipfit.symm     - distance (mm) for symmetry constraints (ECD)
%    dipfit.Lpos     - x,y,z source positions (mm)            (ECD)
%    dipfit.Nm       - number of modes                        (Imaging)
%    dipfit.Ns       - number of sources
%    dipfit.Nc       - number of channels
%
%    dipfit.vol      - volume structure (for M/EEG)
%    dipfit.datareg  - registration structure (for M/EEG)

  			struct with fields:

     			sensors: [1×1 struct]
     			fid_eeg: [1×1 struct]
     			fid_mri: [1×1 struct]
       			toMNI: [4×4 double]
     			fromMNI: [4×4 double]
    			modality: 'EEG'

%	dipfit.sens

  			struct with fields:

     			chanpos: [21×3 double]
     			elecpos: [21×3 double]
    			chantype: {1×21 cell}
    			chanunit: {1×21 cell}
       			label: {1×21 cell}
        		unit: 'mm'

%	dipfit.rad - default is 16 mm
% 	dipfit.G - {1×m} cell{i}, where G{i} = L(:,Ip)*U , where i=1:4 and U = rotation matrix from SVD on part of the lead field matrix
% 	dipfit.U - {1×m} cell, singular vectors
% 	dipfit.Ip - {1×m} cell
% 	dipfit.Nd - number of dipoles
% 	dipfit.gainmat -  Lead field filename

```

### Questions:
- How are the Lpos defined? Is there a sort of prior which is then adapted according to the head model?

- About DCM.M.dipfit:
	- dipfit.location : what does setting it to zero mean? That we are not estimating the locations? That they are fixed?
	- dipfit.type: What are the difference?
		- 'ECD': equivalent current dipole? "parameterised lead field"
		- 'LFP': "LFP electrode gain". OK, so specific forward model for LFP.
		- 'IMG': "Imaging solution"?? What is this option? Why is it default?
	- dipfit.Nm: what are the modes?
	- dipfit.Nc; number of GOOD channels?
	- dipfit.vol: head model? Age dependent?
	- dipfit.datareg: what is this?
	- dipfit.rad: radius for the sources?
	- dipfit.Nm: still don't get why default of 6 is ok.
- #194: create MSP spatial basis set in source space --> What is happening here?
	- What is vert?
	- What is Dp?
- #202: How is Ip helpful? What is going on here?



## Function dissection `spm_dcm_eeg_channelmodes`
Returns the channel eigenmodes.
Uses SVD (an eigensolution) to identify the patterns with the greatest prior covariance; assuming independent source activity in the specified spatial (forward) model. 

```
% FORMAT [U] = spm_dcm_eeg_channelmodes(dipfit,Nm) % OUR USAGE
% FORMAT [U] = spm_dcm_eeg_channelmodes(dipfit,Nm,xY)
% dipfit  - spatial model specification
% Nm      - number of modes required (upper bound)
% xY      - data structure
% U       - channel eigenmodes
```

### Questions:

- Nm : here 7 and regarded as an upper bound? Why is it different?
- #33: what is happening?...
- #40: why SVD of L*L'?
- #70: re-scale spatial projector --> Why U = U/sqrt(mean(S)) ?


## Important vocabulary:
- **ECD** = A summation of currents of many neurons with the same positive-negative direction can be mimicked as one strong dipole. This is termed the equivalent current dipole (ECD). From [here](https://link.springer.com/referenceworkentry/10.1007%2F978-3-540-29805-2_1361).
- **LFP**: The Local Field Potential (LFP) is the electric potential recorded in the extracellular space in brain tissue, typically using micro-electrodes (metal, silicon or glass micropipettes). LFPs differ from the EEG, which is recorded at the surface of the scalp, and with macro-electrodes. It also differs from the electro-corticogram (EcoG), which are recorded from the surface of the brain using large subdural electrodes, while LFPs are recorded in depth, from within the cortical tissue (or other deep brain structures).
Besides their invasive aspect, LFPs also sample relatively localized populations of neurons, as these signals can be very different for electrodes separated by 1 mm (Destexhe et al., 1999) or by a few hundred microns (Katzner et al., 2009). In contrast, the EEG samples much larger populations of neurons (Niedermeyer and Lopes da Silva, 1998). The difference is due to the fact that the EEG signals must propagate through various media, such as cerebrospinal fluid, dura matter, cranium, muscle and skin, and are therefore much more subject to filtering and diffusion phenomena across these media. However, even if recorded close to the neuronal sources, LFP signals are also filtered, because the recording electrode is separated from the sources by portions of cortical tissue. Besides these differences, EEG and LFP signals display the same type of oscillations during wake and sleep states (Steriade, 2003). From [Scholarpedia](http://scholarpedia.org/article/Local_field_potential).