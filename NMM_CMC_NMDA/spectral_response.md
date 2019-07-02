# Understanding how the spectral response of a NMM is generated in SPM

`m` represents the number of sources.

`p` is the number of cell populations in each source. Given that we are considering the implementation with the canonical microcircuit: `p=4`.

`u` is the number of inputs.

`c` is the number of sensor channels.

`nf` is the number of analyzed frequencies.

## Function dissection: [spm_csd_mtf.m](https://tnurepository.ethz.ch/inesb/anti-nmda/blob/master/src/preproc_and_DCM/src/spm12/toolbox/dcm_meeg/spm_csd_mtf.m)

From the function documentation: *When called with U this function will return a cross-spectral response for each of the condition-specific parameters specified in U.X; otherwise it returns the complex CSD for the parameters in P (using the expansion point supplied in M.x).*

M.x contains the hidden states! In our case, the membrane voltage and the conductances for all three receptors AMPA, NMDA and GABA.

### Function outline:
- Check for experimental inputs (none in our model);
- Define frequencies of interest;
- Check number of channels (7 in our case)
    - COMMENT: this part is also supposed to, according to the documentation, get exogenous (neuronal) inputs or sources. Instead, it stores the number of different frequencies which are being analyzed (see [here](https://tnurepository.ethz.ch/inesb/anti-nmda/blob/master/src/preproc_and_DCM/src/spm12/toolbox/dcm_meeg/spm_csd_mtf.m#L72)).
- Obtain spectrum of innovations (Gu) and noise (Gs and Gn)
    - Calls [spm_csd_mtf_gu.m](https://tnurepository.ethz.ch/inesb/anti-nmda/blob/master/src/preproc_and_DCM/src/spm12/toolbox/dcm_meeg/spm_csd_mtf_gu.m) and gets:
		- `Gu (nf by m)`: spectrum of neuronal innovations multiplied with DCT
		- `Gs (nf by 1)`: spectrum of channel noise (specific: with the same exponent)
		- `Gn (nf by 1)`: spectrum of channel noise (non-specific)
		- **DON'T UNDERSTAND:** Why do we need Gs *and* Gn?
- Loops over trials (experimental conditions) and condition-specific parameters
	- Since we don't have any, `Q` is the same as `P`
	- In `M.x = spm_dcm_neural_x(Q,M)`, `M.x` does not get changed.
		- **DON'T UNDERSTAND:** this function is supposed to *return the fixed point or steady-state of a neural mass DCM*. From the code, we are not applying it because M.f (in our case `spm_fx_cmm_nmda.m` is not included in the cases defined in the function: `spm_fx_cmm` and `spm_fx_mfm`.
	- Compte transfer function (Laplace transform of the impulse response of an LTI system when initial conditions are zero)
		- [This](https://tnurepository.ethz.ch/inesb/anti-nmda/blob/master/src/preproc_and_DCM/src/spm12/spm_dcm_mtf.m#L68) is where `spm_fx_cmm_nmda.m` gets called!
		- **DON'T REALLY UNDERSTAND THIS STEP.**
	- Predicts cross spectral density `G`
		- **DON'T UNDERSTAND:** `G(i,:,:) = sq(S(i,:,:))*diag(Gu(i,:))*sq(S(i,:,:))'`
			- What formula is being used here? I understand that we are iterating over the frequencies.
- Add channel noise
	- Add channel specific noise: we only add `Gs` to the diagonal terms of the predicted CSD
		- **DON'T UNDERSTAND:** why? What does this say about the noise being specific?
		- And, given the dimensions of `Gs`, the noise level seems to be specific for each frequency.
	- Add cross-spectral density from common channel noise: affects all terms for predicted CSD (not just the diagonal terms!)


## Function dissection: [spm_csd_mtf_gu.m](https://tnurepository.ethz.ch/inesb/anti-nmda/blob/master/src/preproc_and_DCM/src/spm12/toolbox/dcm_meeg/spm_csd_mtf_gu.m)

From the function documentation (c here in not the `c` defined above! Figure this out!)
- pE.a(2,m) - neuronal fluctuations        - amplitude and exponent
- pE.b(2,c) - channel noise (non-specific) - amplitude and exponent
- pE.c(2,c) - channel noise (specific)     - amplitude and exponent
- pE.d(8,m) - neuronal fluctuations        - basis set coefficients

### Function outline:
- Gets number of sources and frequencies analyzed.
- Generates spectrum of neuronal innovations `Gu`
    - **Loops** over sources and computes, for the i-th source: `Gu(:,i) = exp(P.a(1,i))*f.^(-exp(P.a(2,i)))`
        - Comments:
            - Positivity constraint imposed on amplitude → scalar!
            - Negativity constraint imposed on exponent → scalar!
            - Hence, output is: `A*(1/f^B)`, `f` is a vector containing the analyzed frequencies.
    - **Output**: `Gu` is `5 by 4` → neuronal innovations per analyzed frequency, per source.
- Computes discrete cosine set (DCT) of order 8 (in our SPM version) and 4 (in [SPM12](https://github.com/spm/spm12/blob/master/toolbox/dcm_meeg/spm_ssr_priors.m#L53))
    - **Reminder**: `y` is the data, `C` is represented by `X` in the code, and `x` is our `d`!

	- Dimensions:
        - `X` is `5 by 9`
        - `d` is `8 by 4`
        - `Mu` is `5 by 4`
	- **DON'T UNDERSTAND:** `Mu = exp(X(:,2:end)*P.d)`
  	  - Why are we ignoring the first column?
  	  - Why the exponential?

<p align="center">
  <img width="600" height="350" src="dct.png">
</p>

**Source**: Meyer-Baese and
Schmid, *Pattern Recognition and Signal Analysis in Medical Imaging*, 2014.

- Then: `Gu = Gu.*Mu;`
	- **DON'T UNDERSTAND:** Why are we doing this elementwise multiplication?
- Generate spectra of specific (P.c) and nonspecific (P.d) channel noise: 
    - For `Gn` and `Gs` : same general observations as those for the neuronal innovations
	- `size(Gn) = size(Gs) = [nf,1]`
    - **DON'T UNDERSTAND:** 
        - What is meant by `(specific: with the same exponent)`??
		- Why is `Gs` computed so: `Gn  = exp(P.b(1) - 2)*f.^(-exp(P.b(2)))`
			- What's with the `-2`? (same goes for `Gn`!)
		- Why do we need 2 terms which basically the same thing?



