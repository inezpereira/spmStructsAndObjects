## Neural mass model with CMC and NMDA parameters

In the model, you will find the following substruct multiple times, which will be called `model_definition`. 
This set of parameters needs to appear in the priors and constitutes, for instance, the posterior estimate substruct `DCM.Ep`.

`m` stands for the number of sources which are modelled.

```
Ep
├─── S                              # population variance.
├─── T: [m×3 double]                # time constants for AMPA, GABA and NMDA channels
├─── G                              # intrinsic connectivity
├─── GN_intrin: [m×1 double]        # input scale to NMDA for each of the m sources. Pyramidal NMDA?? Superficial/deep?
├─── GA_intrin: [m×1 double]        # input scale to AMPA for each of the m sources.
├─── GG_intrin: [m×1 double]        # input scale to GABA for each of the m sources.
├─── GNi_intrin: [m×1 double]       # input scale to interneurons NMDA
├─── GAi_intrin: [m×1 double]       # Mg-switch sigmoid scale, slope and sensitivity 
├─── GGi_intrin: [m×1 double]       # input scale to GABA for each of the n sources
├─── CV: [1×m double]               # membrane capacitance for all n sources
├─── E                              # background noise
├─── A                              # extrinsic connections for AMPA (forward {1} and backward {2} connections between sources, row: to, col: from)
├─── AN                             # extrinsic connections for NMDA (same shape as A)
├─── C                              # subcortical input
├─── H                              # intrinsic connectivity. Unused? Synaptic densities?
├─── R                              # onset and dispersion
├─── D                              # delays (unused)
├─── Lpos                           # ROIs (unused)
├─── L                              # leadfield
├─── J                              # contributing states
├─── a                              # neuronal innovations?
├─── b                              # channel noise (not source-specific)??
├─── c                              # channel noise (source-specific)??
├─── d                              # channel noise (basis set coefficients)??
```

And now, I give you the DCM struct:
```
DCM
├─── M
|    ├─── P                         # model parameters
|    |    ├─── model_definition
|    ├─── pE                        # prior expectation
|    |    ├─── model_definition
|    ├─── Nmax
|    ├─── dipfit                    # spatial model specification. Gives dipole structure??
|    |    ├─── model: 'CMM_NMDA'
|    |    ├─── type
|    |    ├─── Ic
|    |    ├─── location
|    |    ├─── symmetry
|    |    ├─── Lpos
|    |    ├─── modality
|    |    ├─── Ns
|    |    ├─── Nc
|    |    ├─── silent_source
|    |    ├─── vol
|    |    |    ├─── bnd
|    |    |    |    ├─── pos
|    |    |    |    ├─── tri
|    |    |    ├─── cond
|    |    |    ├─── mat
|    |    |    ├─── type
|    |    |    ├─── unit
|    |    |    ├─── cfg
|    |    |    |    ├─── method
|    |    |    |    ├─── outputfilepresent
|    |    |    |    ├─── toolbox
|    |    |    |    ├─── callinfo
|    |    |    |    ├─── version
|    |    |    |    ├─── headshape
|    |    |    |    ├─── conductivity
|    |    |    |    ├─── tissue
|    |    |    |    ├─── smooth
|    |    |    |    ├─── threshold
|    |    |    |    ├─── numvertices
|    |    |    |    ├─── isolatedsource
|    |    |    |    ├─── fitind
|    |    |    |    ├─── point
|    |    |    |    ├─── submethod
|    |    |    |    ├─── feedback
|    |    |    |    ├─── radius
|    |    |    |    ├─── maxradius
|    |    |    |    ├─── baseline
|    |    |    |    ├─── singlesphere
|    |    |    |    ├─── tissueval
|    |    |    |    ├─── transform
|    |    |    |    ├─── siunits
|    |    |    |    ├─── headmodel
|    |    |    |    ├─── previous
|    |    |    ├─── skin_surface
|    |    |    ├─── inner_skull_surface
|    |    |    ├─── source
|    |    ├─── datareg
|    |    |    ├─── sensors
|    |    |    |    ├─── chanpos
|    |    |    |    ├─── elecpos
|    |    |    |    ├─── chantype
|    |    |    |    ├─── chanunit
|    |    |    |    ├─── label
|    |    |    |    ├─── unit
|    |    |    ├─── fid_eeg
|    |    |    |    ├─── pnt
|    |    |    |    ├─── fid
|    |    |    |    |    ├─── pnt
|    |    |    |    |    ├─── label
|    |    |    |    ├─── unit:'mm'
|    |    |    ├─── fid_mri
|    |    |    |    ├─── pnt
|    |    |    |    ├─── fid
|    |    |    |    |    ├─── pnt
|    |    |    |    |    ├─── label
|    |    |    |    ├─── unit:'mm'
|    |    |    ├─── toMNI
|    |    |    ├─── fromMNI
|    |    |    ├─── modality: 'EEG'
|    |    ├─── sens
|    |    |    ├─── chantype
|    |    |    ├─── chanunit: {'V', ... , 'V'}
|    |    |    ├─── elepos
|    |    |    ├─── label
|    |    |    ├─── type
|    |    |    ├─── unit: 'mm'
|    |    |    ├─── chanpos
|    |    ├─── siunits
|    |    ├─── G
|    |    ├─── U
|    |    ├─── Ip
|    |    ├─── radius
|    |    ├─── Nm
|    |    ├─── Nd
|    |    ├─── gainmat
|    ├─── IS: 'spm_csd_mtf'                             # Spectral response of a NMM (transfer function x noise spectrum)
|    ├─── FS 
|    ├─── g: 'spm_gx_erp'                               # observer for a neural mass model of event related potentials. Unused?
|    ├─── f: 'spm_fx_cmm_NMDA'                          # calls state equations of motion for canonical neural-mass and mean-field models 
|    ├─── x                                             # neural states. Initialized as zero sparse matrix.
|    ├─── n                                             # total number of neural states. Defined as length(spm_vec(DCM.M.x))
|    ├─── pC                                            # prior (co)variances
|    |   ├─── model_definition
|    ├─── hE                                            # prespecified as 8? Why? What does this represent?
|    ├─── hC                                            # prespecified as 1/128? Why? What does this represent?
|    ├─── m                                             # number of sources
|    ├─── u
|    ├─── U
|    ├─── l
|    ├─── Hz
|    ├─── dt
├─── name: '<name of DCM file>'
├─── xY: [1x1 struct]                                   # data
|    ├─── Dfile: '<path/to/preprocessed/EEG/data>'
|    ├─── y
|    ├─── xy
|    ├─── modality: 'EEG'
|    ├─── name
|    ├─── Ic
|    ├─── Time
|    ├─── dt
|    ├─── coord2D
|    ├─── pst
|    ├─── It
|    ├─── nt
|    ├─── code
|    ├─── scale
|    ├─── X0
|    ├─── R
|    ├─── Hz
|    ├─── csd
|    ├─── orig_data_size
|    ├─── inds_used_size2
|    ├─── csd_per_trial
|    ├─── U
|    ├─── Q
├─── options
|    ├─── trials
|    ├─── analysis: 'CSD'
|    ├─── model: 'CMM_NMDA'           # 'ERP', 'SEP', 'CMC', 'LFP', 'NMM' or 'MFM'
|    ├─── spatial: 'IMG'              # 'ECD', 'LFP' or 'IMG'     (see spm_erp_L)
|    ├─── Tidcm                       # [start end] time window in ms
|    ├─── Fdcm                        # [start end] Frequency window in Hz
|    ├─── Nmodes                      # number of spatial modes???
|    ├─── D                           # time bin decimation       (usually 1 or 2)??
├─── Lpos
├─── Sname: {'S1', 'S2, ... }                         # source names
├─── A: {[m×m double]  [m×m double]  [m×m double]}    # binary constraints on the extrinsic (between source) connections. 3 cell entries because I am modelling the activity of three channels??
├─── C:m×0 empty sparse double matrix # binary constraints on the regions which receive external input. In this case, we are collecting resting-state data, hence the zero.
├─── B                                # binary constraints on the modulatory connections for each of the m conditions.
├─── xU                               # design
|    ├─── X
├─── val
├─── dtf                              # directed transfer functions (source space)
├─── ccf                              # cross covariance functions (source space)
├─── coh                              # cross coherence functions (source space)
├─── fsd                              # specific delay functions (source space)
├─── pst                              # peristimulus time
├─── Hz                               # frequency (vector with integer valuesof the analyzed frequency spectrum, e.g. if 2-10 Hz, then DCM.Hz is the same as the vector [2:10].
├─── Ep                               # conditional expectation. Meaning your posterior estimates of the model parameters??
|    ├─── model_definition
├─── Cp                               # conditional covariance. posterior covariance matrices??
├─── Pp                               # conditional probability. posterior probability of each parameter??
|    ├─── model_definition
├─── Hc                               # conditional responses (y), channel space. Model estimates for the generated data??
├─── Rc                               # conditional residuals (y), channel space. Residuals??
├─── Hs                               # conditional responses (y), source space
├─── Ce                               # eML error covariance
├─── Ce_Eh
├─── F                                # Laplace log evidence
├─── ID                               # data ID

```

## Resources:
- [spm_dcm_csd.m](https://github.com/spm/spm12/blob/master/toolbox/dcm_meeg/spm_dcm_csd.m)
- [spm_dcm_neural_priors.m](https://github.com/spm/spm12/blob/master/toolbox/dcm_meeg/spm_dcm_neural_priors.m)
  - Because priors are specified under log normal assumptions, most parameters are simply scaling coefficients with a prior expectation and variance of one.  After log transform this renders `pE = 0` and `pC = 1`;
  - Defines prior moments on the parameters with [spm_cmc_priors.m](https://github.com/spm/spm12/blob/master/toolbox/dcm_meeg/spm_cmc_priors.m) or accepts user input.
  - Defines priors on the spatial model with [spm_L_priors.m](https://github.com/spm/spm12/blob/master/toolbox/dcm_meeg/spm_L_priors.m) or accepts user input.
  - Defines initial states and equations of motion with [spm_dcm_x_neural.m](https://github.com/spm/spm12/blob/master/toolbox/dcm_meeg/spm_dcm_x_neural.m)
  - Defines initial states and equations of motion through [spm_dcm_csd.m](https://github.com/spm/spm12/blob/master/toolbox/dcm_meeg/spm_dcm_csd.m).
- [spm_erp_L.m](https://github.com/spm/spm12/blob/master/toolbox/dcm_meeg/spm_erp_L.m)
  - The lead field (L) is constructed using the specific parameters in P and, where necessary, information in the dipole structure dipfit. For ECD models P.Lpos and P.L encode the position and moments of the ECD. The field `dipfit.type` ('ECD', 'LFP' or 'IMG') determines whether the model is ECD or not. For imaging reconstructions the paramters `P.L` are a (m x n) matrix of coefficients that scale the contrition of n sources to `m = dipfit.Nm` modes encoded in `dipfit.G`. For LFP models (the default), `P.L` simply encodes the electrode gain for each source contributing a LFP.
  
## Special thanks
I want to thank Moritz Gruber for helping me get started on this and sharing his notes and thoughts with me. It made searching through the spm repository a much easier task!
