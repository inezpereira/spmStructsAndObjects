# Default parameter values for prior expectation and prior covariance

`m` represents the number of sources.

I will use common Matlab functions to more concisely express what the parameters are.

## Prior Expectation

| Field  | Meaning | Value  | Questions or comments| Script with documentation about variable
|:----------|:----------|:----------|:----------|:----------|
| S    | population variance | 0   | 
| T   |time constants for AMPA, GABA and NMDA channels. One row for each source.  | `zeros(m,3)`   | 
| G | intrinsic connectivity |`zeros(m,1)` | Why one value per source? What does this represent really?|
| GN_intrin | input scale to NMDA for each of the m sources. | `zeros(m,1)` | Same parameters for all cells containing NMDA receptor? Or just for pyramidal cells? (see the paramters with "i")|
| GA_intrin | input scale to AMPA for each of the m sources |  `zeros(m,1)` | Idem|
| GG_intrin | input scale to GABA for each of the m sources.| `zeros(m,1)` | Idem |
| GNi_intrin | input scale to interneurons NMDA | `zeros(m,1)` | Now just interneurons? Does it overwrite a previously defined value, like GN_intrin?|
| GAi_intrin | Mg-switch sigmoid scale, slope and sensitivity | `zeros(m,1)` | Shouldn't this be for NMDA as well? Why does it share the notation for the AMPA input scale?|
| GGi_intrin | input scale to GABA for each of the m sources.| `zeros(m,1)` | Only for interneurons? |
| CV | membrane capacitance for all m sources | `zeros(1,m)`|
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



## Prior covariance

We now turn to the covariance parameter of these. Since the the meaning of the parameters stays the same, we've left out the 'meaning' column.

| Field  | Value  | Questions or comments| Script with documentation about variable
|:----------|:----------|:----------|:----------|
| S    		| 0.0156 | Why this particular value? How was it found?
| T | `0.0625*ones(m,3)` | Idem
| G | `zeros(m,	1)` | Zero expectation and zero variance?? Where is within source connectivity defined?|
| GN_intrin | `0.1250*ones(m,1)`| Why this value?|
| GA_intrin | `0.1250*ones(m,1)`| Idem|
| GG_intrin | `0.1250*ones(m,1)`| Idem|
| GNi_intrin | `0.1250*ones(m,1)`| Idem|
| GAi_intrin |`0.1250*ones(m,1)`| Idem|
| GGi_intrin | `0.1250*ones(m,1)`| Idem|
| CV | `zeros(1,m)` | Zero expectation and zero variance?? How can I always have membrane capacitance?|
| E | 0.0078125 | Why this value?|
| A | `{1×2 cell}`, each cell: `mxm double`, with `0` if no connection established and `0.1250` if connection established. | So `0` covariance for the expected value `-32`? Again, why this value? And why fix it? |
| AN | Idem | Idem
| C | `[]`
| H | `zeros(m, m, m)` 
| R | `[]`
| D | `diag(repmat(0.0312, m,1))`| Why this value?
| Lpos | `[]`
| L | `64*ones(6,m)` | Why 64?
| J | `zeros(1,16)`, expect for `(1,3)=0.0312` and `(1,4)=0.0312`| Why this value?
|a | `0.0078125*ones(2,m)` | Why?
|b | `0.0078125*ones(2,1)` | Why?
|c | Idem | Idem
|d |`0.0078125*ones(8,m)`| Why this particular value? Why this first dimension?
