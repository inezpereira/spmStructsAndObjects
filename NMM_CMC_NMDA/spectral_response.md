# Understanding how spectral response of a NMM is generated in SPM

## Function dissection: [spm_csd_mtf](https://tnurepository.ethz.ch/inesb/anti-nmda/blob/master/src/preproc_and_DCM/src/spm12/toolbox/dcm_meeg/spm_csd_mtf.m)

From the function documentation: *When called with U this function will return a cross-spectral response for each of the condition-specific parameters specified in U.X; otherwise it returns the complex CSD for the parameters in P (using the expansion point supplied in M.x).*

M.x contains the hidden states! In our case, the membrane voltage and the conductances for all three receptors AMPA, NMDA and GABA.

Function outline:
- Check for experimental inputs (none in our model);
- Define frequencies of interest;
- Check number of channels (7 in our case)
    - COMMENT: this part is also supposed to, according to the documenation, get exogenous (neuronal) inputs or sources. Instead, stores the number of different frequencies which are being analyzed.