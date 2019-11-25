# TIPsort cheat sheet

This document contains tips and tricks for using TIPsort (https://github.com/e-j-w/TIPsort).

## Suppression and charge parameters

For the 22Ne and 28Mg dataset, suppression was performed online, supLow=4000 and supHigh=5000 is acceptable.  useCharge=1.

## Doppler shift grouping

DS grouping requires the `Doppler_shift_group_map.par` parameter file generated using the `tree2doppler_map` or `tree2doppler_2Dmap` codes from FileConvTools (https://github.com/e-j-w/FileConvTools).

## Making gated spectra

### No Doppler correction

Ring grouped, gate bounds in keV:

```
Tigress_ECalABSuppSumEGated master_file_name supLow supHigh gateELow gateEHigh
```

DS grouped, gate bounds in keV:

```
TigressCsIArray_ECalABSuppSumEGated_Group master_file_name supLow supHigh gateELow gateEHigh
```

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
