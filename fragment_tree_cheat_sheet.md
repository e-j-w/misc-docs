# GRSISort fragment tree cheat sheet

This document contains tips and tricks for using GRSISort (https://github.com/GRIFFINCollaboration/GRSISort) fragment trees.

## Loading the fragment tree file

The fragment tree data needs to be loaded into GRSISort for any of this to work.

```
grsisort -l /path/to/fragmentRUN_000.root
```

### Fragment vs. bad fragment tree

Events which fail to sort are placed in the `BadFragmentTree` rather than the `FragmentTree` in the fragment tree ROOT file.  To inspect these events, replace `FragmentTree` in any of the commands listed below with `BadFragmentTree`.

## Drawing a hit pattern

For channels 0 through 1000:

```
FragmentTree->Draw("GetChannelNumber()>>(1000,0,1000)","","colz")
```

## Drawing a time series

The normal timestamps reset every 12 hours.  To plot DAQ timestamps which do not reset, first run:

```
FragmentTree->Scan("fDaqTimeStamp","","colsize=20")
```

This gives you the number of DAQ timestamps in each channel.  Then you can draw a time series.  For example, if there are 1572649571 DAQ timestamps, the time series for energy in channel 722 is drawn using:

```
FragmentTree->Draw("GetEnergy():(fDaqTimeStamp-1572649571)/60>>(1000,0,10000,4096,0,4096)","GetChannelNumber()==722","colz")
```

with a plot range of [0:10000] on the energy axis and [0:4096] on the time axis.

To plot channel number vs. DAQ timestamp, one could use:

```
FragmentTree->Draw("GetChannelNumber():(fDaqTimeStamp-1572649571)/60>>(1000,0,3000,1000,0,1000)","","colz")
```

## Energy vs. channel (or any other 2D plot)

For calibrated data (calibration parameters from the cal file are applied to both fragment and analysis trees), energy is in units of keV.


```
FragmentTree->Draw("GetChannelNumber():GetEnergy()>>(5000,0,5000,1000,0,1000)","","colz")
```

Here, energy is on the x axis (range 0 to 5000, in keV if calibrated), and channel is on the y axis (range 0 to 1000).