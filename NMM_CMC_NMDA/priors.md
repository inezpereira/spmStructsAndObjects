# Default parameter values for prior expectation and prior covariance

`m` represents the number of sources.

I will use common Matlab functions to more concisely express what the parameters are.


| Field  | Meaning | Value  | Questions or comments| Script with documentation about variable
|:----------|:----------|:----------|:----------|:----------|
| S    | population variance | 0   | 
| T   |time constants for AMPA, GABA and NMDA channels. One row for each source.  | `zeros(m,3)`   | 
| G | intrinsic connectivity |`zeros(m,1)` | Why one value oer source? What does this represent really?|
| GN_intrin | input scale to NMDA for each of the m sources. | `zeros(m,1)` | Same parameters for all cells containing NMDA receptor? Or just for pyramidal cells? (see the paramters with "i")|
| GA_intrin | input scale to AMPA for each of the m sources |  `zeros(m,1)` | Idem|
| GG_intrin | input scale to GABA for each of the m sources.| `zeros(m,1)` | Idem |
| GNi_intrin | input scale to interneurons NMDA | `zeros(m,1)` | Now just interneurons? Does it overwrite a previously defined value, like GN_intrin?|
| GAi_intrin | Mg-switch sigmoid scale, slope and sensitivity | `zeros(m,1)` | Shouldn't this be for NMDA as well? Why does it share the notation for the AMPA input scale?|
| GGi_intrin | input scale to GABA for each of the m sources.| `zeros(m,1)` | Only for interneurons? |
| CV | membrane capacitance for all n sources | `zeros(1,m)`|
| E | background noise | 0 |
| A | extrinsic connections for AMPA (forward {1} and backward {2} connections between sources, row: to, col: from) | `{1×2 cell}`, each cell: `mxm sparse double`, with `-32` if no connection established and `0` if connection established. | How does it know? Where to find this operation? Why `-32`?
| AN | extrinsic connections for NMDA (same shape as A) | idem | idem|
| C | subcortical input | `[]` | If dealing with resting-state EEG.
| H | intrinsic connectivity. | `zeros(m, m, m)`| Unused? Synaptic densities?
| R | onset and dispersion |  `[]` | Actual meaning?
| D | delays (unused) | `zeros(m, m)`| Why unused? Why this value?
| Lpos | ROIs (unused) | `[]` | Why unused? When is it used?
| L | leadfield | `zeros(6,m)`| What is this 6??
| J | contributing states |`zeros(1,16)`, expect for `(1,2)=1`| What is this?
|a |neuronal innovations? |`zeros(2,m)`| What is this, really? Why these dimensions?
|b | channel noise (not source-specific) |`zeros(2,1)`| 2 channels?
|c | channel noise (source-specific) |`zeros(2,1)`| Understand dimensions.
|d | channel noise (basis set coefficients) |`zeros(8,m)`| Why is the first dimension set to 8?


