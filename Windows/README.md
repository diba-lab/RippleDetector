# Building Ripple Detector in Windows
This module provides more specific instructions for building the Ripple Detection module in Windows and fills in some important (and frustrating) gaps left in the OpenEphys wiki.

## Build GUI from source
Head [here](https://open-ephys.atlassian.net/wiki/spaces/OEW/pages/491621/Windows) for instructions on how to download the OpenEphys Source code and compile it. Follow Steps 1-6 to a t.  
- For step 7, before running first open up the CMakeList.txt file in the top-level folder in you plugin-GUI repository and comment out lines 17-19 with a #.  
Then follow the rest of the steps to build the GUI from source.  <b> Note that the "Debug" version is super slow in Windows so you should build the "Release" version and run the open-ephys.exe file from the "Release" folder.</b>

## Build the Ripple plugin from source
 Go to the [Open Ephys wiki website](https://open-ephys.atlassian.net/wiki/spaces/OEW/pages/950297/Tutorial+Add+a+custom+processor) for instructions on building the plugin from source and then tweak these steps as follows:  
- 1) Copy the entire RippleDetector folder into the Plugins folder. 
- 2) Make sure Visual Studio has the correct .cpp, .h, and OpenEphys.lib files and their correct locations for the RippleDetector (see 2 below).  
- 5) See #5 below if you get any errors.


## Building a custom plugin from source
I know this doesn't belong here but it's the best place for it for now.  
  
Go to the [Open Ephys wiki website](https://open-ephys.atlassian.net/wiki/spaces/OEW/pages/950297/Tutorial+Add+a+custom+processor) for instructions on building the plugin from source. Do them <b>IN ORDER</b> and then tweak these steps as follows:  
- 1) Don't use the ExampleProcessor but rather use the GenericProcessor in the Source/Processors folder or the PhaseDetector in the Plugins folder to start and rename the folder to match your custom plugin.  
- 2) To add files, first copy the .cpp, .h, and OpenEphysLib.cpp files over to the Plugins directory, rename them to match you new module, then open the open the open-ephys.vcxproj folder in Visual Studio, find your plugin in the "Solution Explorer" (Ctrl+Alt+L or View->Solution Explorer) & right click on the "Solution 'open-ephys-GUI'". Then remove all header and source files in the tree, right click to add a new item, and select the newly renamed files. Make <b>SURE</b> to change the display name in the OpenEphys.lib file (e.g. "info->name = 'MyPlugin'").  
- 5) Upon building, Visual Studio creates DLL files that sometimes, for some reason, don't end up with the right name.  You might have to manually adjust.  To do so, a) Open the Property Manager (View->Other Windows->Property Manager), b) Right click on "Release|x64" and hit "Properties".   
![Image of Change Screen](https://github.com/diba-lab/RippleDetector/blob/master/Windows/How%20to%20get%20to%20screen%20to%20change%20plugin%20DLL%20output%20name.JPG)
