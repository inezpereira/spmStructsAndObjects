# Analysis of DCM struc in SPM 
A community-fed documentation for the DCM structs available on SPM12.
It's still a work in progress and heavily biased torwards the types of models I am dealing with presently, so contributions are very welcome.

## Abbreviations and resources: 📖
- SPM: Statistical Parametric Mapping
    - [SPM on Scholarpedia](http://www.scholarpedia.org/article/SPM)
- DCM: Dynamic Causal Modeling
    - If you are not familiar with this concept, consider reading [this article on Scholarpedia](http://scholarpedia.org/article/Dynamic_causal_modeling)
- EEG: Electroencephalography/Electroencephalogram
    - [EEG on Scholarpedia](http://scholarpedia.org/article/Electroencephalography)
    - [Functional imaging on Scholarpedia](http://scholarpedia.org/article/Functional_imaging)
- fMRI: functional Magnetic Resonance Imaging
    - [fMRI on Scholarpedia](http://scholarpedia.org/article/Functional_magnetic_resonance_imaging)
- NMM: Neural mass model
- MFM: Mean Field model
- NMDA: N-Methyl-D-aspartic acid. Often, you will see NMDA alone in the documentation. However, what is usually meant is the NMDA receptor
    - The Morris-Lecar model was expanded in 2010 to include NMDA ion channels in pyramidal cells and inhibitory interneurons. For details, please consult the paper by [Moran _et al_, 2010](https://library.mpib-berlin.mpg.de/ft/ext/rd/RD_Consistent_2011.pdf)
- CMC: canonical microcircuit
    - [Douglas, Martin, and Whitteridge, (1989). A canonical microcircuit for neocortex. Neural Comput. 1, 480–488.](https://www.researchgate.net/publication/242918941_A_Canonical_Microcircuit_for_Neocortex)
    - [Bastos, Usrey, Adams, Mangun, Fries, and Friston (2012). Canonical Microcircuits for Predictive Coding. Neuron 76](https://www.cell.com/neuron/fulltext/S0896-6273(12)00959-2?_returnURL=https%3A%2F%2Flinkinghub.elsevier.com%2Fretrieve%2Fpii%2FS0896627312009592%3Fshowall%3Dtrue)

## Feel like contributing? Amazing! 🎉
If you want to contribute, please regard the following rules:
- Keep the hierarchy, folder-like, formatting as is. Or create an issue if you have a better suggestion!
- If the type of a parameter is known but dimensions vary, write: `parameter: [ __×__ double ]`
- Comments to a single field of the struct should preferably be written as inline comments next to the specific field. If they are too long, create a footnote.
