## Neural mass model with CMC and NMDA parameters

```
DCM
├─── M
|    ├─── P
|    |    ├─── S
|    |    ├─── T
|    |    ├─── G
|    |    ├─── GN_intrin
|    |    ├─── GA_intrin
|    |    ├─── GG_intrin
|    |    ├─── GNi_intrin
|    |    ├─── GAi_intrin
|    |    ├─── GGi_intrin
|    |    ├─── CV
|    |    ├─── E
|    |    ├─── A
|    |    ├─── AN
|    |    ├─── C
|    |    ├─── H
|    |    ├─── R
|    |    ├─── D
|    |    ├─── Lpos
|    |    ├─── L
|    |    ├─── J
|    |    ├─── a
|    |    ├─── b
|    |    ├─── c
|    |    ├─── d
|    ├─── pE
|    |    ├─── S
|    |    ├─── T
|    |    ├─── G
|    |    ├─── GN_intrin
|    |    ├─── GA_intrin
|    |    ├─── GG_intrin
|    |    ├─── GNi_intrin
|    |    ├─── GAi_intrin
|    |    ├─── GGi_intrin
|    |    ├─── CV
|    |    ├─── E
|    |    ├─── A
|    |    ├─── AN
|    |    ├─── C
|    |    ├─── H
|    |    ├─── R
|    |    ├─── D
|    |    ├─── Lpos
|    |    ├─── L
|    |    ├─── J
|    |    ├─── a
|    |    ├─── b
|    |    ├─── c
|    |    ├─── d
|    ├─── Nmax
|    ├─── dipfit
|    |    ├─── model
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
|    ├─── IS
|    ├─── FS
|    ├─── g
|    ├─── f
|    ├─── x
|    ├─── n
|    ├─── pC
|    ├─── hE
|    ├─── hC
|    ├─── m
|    ├─── u
|    ├─── U
|    ├─── l
|    ├─── Hz
|    ├─── dt
├─── name
├─── xY
├─── options
├─── Lpos
├─── Sname
├─── A
├─── C
├─── B
├─── xU
├─── val
├─── dtf
├─── ccf
├─── coh
├─── fsd
├─── pst
├─── Hz
├─── Ep
├─── Cp
├─── Pp
├─── Hc
├─── Rc
├─── Hs
├─── Ce
├─── Ce_Eh
├─── F
├─── ID

```
