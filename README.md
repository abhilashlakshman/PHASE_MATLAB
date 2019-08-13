# README #

### PHASE ###
This project was developed as a replacement for an Excel macro in use
by the Shafer Lab, 2018-2019. The current working version of both the MATLAB app and the compiled standalones is 4.2.

This is a MATLAB GUI that reads .txt files output from TriKinetics activity monitors and does activity, sleep, and entrainment analysis on the file data. It outputs the results in Excel files and MATLAB plots in both pdf and fig formats.

### Getting Started ###

The easiest way to use the PHASE program is to install one of the pre-compiled program versions. Open the correct version for your OS (Windows or Mac), and the correct version of the MATLAB runtime engine and required support packages will be downloaded and installed.

To run as a MATLAB app, install the .mlappinstall file. This requires **MATLAB v2018b** or later, as well as the **MATLAB Signal Processing Toolbox** (in order to do the latency and slope analysis types that require smoothing functions) and the **MATLAB Financial Toolbox** (because for some reason this is where the nice graphical calendar-style date picker for specifying experiment start time resides).

If running from source code, the main file is **PHASE.m**. All processing is done by a hierarchy of analysis classes, contained in the SleepyFlies folder.


#### Data Files ####
A sample set of TriKinetics data files are included in the repository. These are .txt files with a name in the format of RunNameMxxxCyy.txt, where RunName is a user-specified run name, Mxxx is the character M followed by a 3-digit board specification number, and Cyy is the character C followed by a 2-digit channel specification number. The rows of data in the files are as follows:
* Run name and run date
* Number of data lines
* Data collection interval (in minutes) for each line of data
* Run start time
* All subsequent rows are data lines representing the number of beam crosses for the fly in a data interval, where the first line is the first data interval (starting at the run start time)


### Programmer notes ###

The analysis program is written as a hierarchy of classes, with each layer building on previous layers.

* DataRaw is the lowest-level class and holds basic file-level information: file location and name(s), boards, and channels specified for use, as well as the raw data from these files.

* DataExperiment adds the user-specified experiment parameters to the DataRaw class (day length, hours of light, start time, etc.) and provides functions to access only the data used during the experiment timeframe.

* DataForAnalysis adds fields to describe the desired analysis and functions to support common tasks across all further analyses: data binned based on specified time interval, data shifted for day-centered plotting, data arranged for plotting based on selected averaging and normalization type, and labels for plots and spreadsheets.

  DataForAnalysisAS and DataForAnalysisSmoothed both extend DataForAnalysis.

  * DataForAnalysisAS provides the functionality for the standard activity/sleep analysis.

  * DataForAnalysisSmoothed add fields for the smoothing function parameters as well as the smoothed data.

    DataForAnalysisPhase and DataForAnalysisLatency both extend this class.

    * DataForAnalysisPhase adds the parameters and plotting and saving functions for phase analysis.

    * DataForAnalysisLatency adds the paramters and plotting and saving functions for latency/anticipation analysis.


Most individual .m files include a detailed header section describing their use and functionality.

PHASE.prj is the project file for the MATLAB app installer.
PHASE_Mac.prj and PHASE_Win.prj are the project files for the standalones for Mac and Windows, respectively. 


### Contact Details ###

This program was primarily developed by Abbey Roelofs, University of Michigan LSA Technology Services.
Email lsait-ars@umich.edu for future assistance with this program.