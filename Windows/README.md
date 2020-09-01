# Building Ripple Detector in Windows
This module provides more specific instructions for building the Ripple Detection module in Windows and fills in some important (and frustrating) gaps left in the OpenEphys wiki.

## Build GUI from source
Head [here](https://open-ephys.atlassian.net/wiki/spaces/OEW/pages/491621/Windows) for instructions on how to download the OpenEphys Source code and compile it. Follow Steps 1-6 to a t.  
- For step 7, before running first open up the CMakeList.txt file in the top-level folder in you plugin-GUI repository and comment out lines 17-19 with a #.  
Then follow the rest of the steps to build the GUI from source.  <b> Note that the "Debug" version is super slow in Windows so you should build the "Release" version and run the open-ephys.exe file from the "Release" folder.</b>

## Build the plugin from source
 You will find detailed instruction in the [Open Ephys wiki website](https://open-ephys.atlassian.net/wiki/spaces/OEW/pages/950297/Tutorial+Add+a+custom+processor).

## Ripple detection algorithm
The ripple detection algorithm works in two steps:
- Calibration: this is the initial stage when threshold for ripple detection is calculated. First, the RMS value is calculated for 1000 consecutive buffer blocks, each block containing a number of "RMS Samples" samples. The final mean and standard deviation (standardDeviation) are obtained and we have the final detection threshold (detectionThreshold) as:

      detectionThreshold = mean + "SDs" * standardDeviation


- Detection: this is when ripples are being identified online. The RMS value of each buffer subblock is calculated and tested against the amplitude threshold. If this value is kept above the amplitude threshold for the time window defined in the parameter "Time Threshold", ripple events are generated. After the event generation, the refractory time starts and new ripple events are detected by the plugin only after this time window ends. Each ripple event is marked on the LFP Viewer as a vertical line.

## Usage
- Use this plugin after a Bandpass Filter block filtered in the ripple band;
- Use this plugin before a sink block (LFP Viewer or Pulse Pal blocks, for instance).

## Plugin interface and parameters set by the user

![Image of RippleDetector](rippleDetector.png)

- Input channel: the number of the input channel from which data will be processed;
- Output channel: the number of the output channel where detection events are marked;
- SDs: number of standard deviations above the average to be the amplitude threshold;
- Time Threshold (ms): the RMS value must be above the amplitude threshold for a minimum of X milliseconds to detect a ripple. X is the value this parameter represents; 
- Refractory Time (ms): represents a time window just after ripple detection in which new ripples are unable to be detected;
- RMS Samples: number of samples inside each buffer subblock to calculate the RMS value.

- Button "Recalibrate": starts the calibration process again, calculating a new amplitude threshold;



