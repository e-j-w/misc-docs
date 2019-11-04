# GRSIsort fragment tree cheat sheet

This document contains tips and tricks for using GRSIsort (https://github.com/GRIFFINCollaboration/GRSISort) fragment trees.

## Fragment vs. bad fragment tree

Events which fail to sort are placed in the `BadFragmentTree` rather than the `FragmentTree`.  To inspect these events, replace `FragmentTree` in any of the commands listed below with `BadFragmentTree`.

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