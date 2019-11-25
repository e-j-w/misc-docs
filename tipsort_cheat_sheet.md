# TIPsort cheat sheet

This document contains tips and tricks for using TIPsort.

## Making gated spectra

### Doppler correction based on CsI ball PID

DS grouped, gate is on Doppler shifted gamma (gate bounds in keV), spectrum is *not* Doppler corrected:

```
TigressCsIArray_ECalABSuppSumDSEGated_GroupPID master_file_name supLow supHigh useCharge gateELow gateEHigh fudge_factor
```

Ring grouped, gate is on Doppler shifted gamma (gate bounds in keV), spectrum is Doppler corrected:

```
TigressCsI_ECalABSuppDSReconstructedSumEGatedPID master_file_name supLow supHigh useCharge gateELow gateEHigh fudge_factor
```

Ring grouped, gate is on Doppler shifted gamma (gate bounds in keV), spectrum is *not* Doppler corrected:

```
TigressCsIArray_ECalABSuppSumDSEGatedPID master_file_name supLow supHigh useCharge gateELow gateEHigh fudge_factor
```
