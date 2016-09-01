HyperSpectral Workflow
=======================

# Modules 

* CalculationWorks.py

    A supporting module for environmental_logger_json2netcdf.py and hyperspectral_metadata.py.
This module is in charge of all the calculation works needed in the
environmental_logger_json2netcdf.py (converting the data made by environmental logger)
and hyperspectral_metadata.py (group up the supporting files for data_raw).

* EnvironmentalLoggerAnalyzer.py

 This module will read data generated by Environmental Sensor and convert to netCDF file.

 Please notice that there are two versions of this module (recognized by their names). The 
 older one will be in charge of the older JSONs; it will be truncated after re-formatting all
 the JSONs.

* hyperspectral_metadata.py

 This module parses JSON formatted metadata and data and header provided by LemnaTec and outputs a formatted netCDF4 file

* DataProcess.py

  We had stopped updating this module; it is now a part of EnvironmentalLoggerAnalyzer.py

* hyperspectral_workflow.sh

  This is the master script for Hyperscpetral workflow. All the scripts above will be called in this script.
NCO/ncap2 script to process and calibrate Terraref exposure data


# Prerequisites Before Deployed

  * VERY IMPORTANT: Please make sure that hyperspectral_workflow.sh, hyperspectral_calibration.nco, hyperspectral_metadata.py, environmental_logger_json2netcdf.py and CalculationWorks.py are in
the same directory. 

  * All the Python scripts syntactically support Python 2.7 and above. Please make sure that the Python in the running environement is
in appropriate version. However, since they also need numpy and scipy and neither of them supports 3.X, hyperspectral workflow normally runs in Python
2.7

  * All the Pythons scripts also rely on the third-party library including: numpy, scipy, netCDF4 and HDF5; they can be installed with either Homebrew
or Macports.

  * Hyperspectral workflow also widely dependes on NCO, a toolkit in dealing netCDF-accessible files, you can get the source code of NCO from Github by
`git clone https://github.com/nco/nco.git` and then come to the directroy and `make install` to install it. It is also available in Homebrew and
Macports by using `brew install nco` or `ports install nco` (macports sometimes requires sudo permission or the installation will fail)

  * Before running the hyperspectral_workflow.sh (the master script), please remember to update the PATH variable by using export command:
`export PATH=$PATH:<the directory of the hyperspectral_workflow.sh script>` or you need to have `bash` in front of each hyperspectral_workflow.sh in commands

# Usage

* CalculationWorks.py

This module will work as a supporting module for EnvironmentalLoggerAnalyzer.py and hyperspectral_metadata.py; it will not be executed
independently except for testing use.

* EnvironmentalLoggerAnalyzer.py

In terminal, use the following command line:

`python ${HOME}/terraref/computing-pipeline/scripts/hyperspectral/environmental_logger_json2netcdf.py /projects/arpae/terraref/raw_data/ua-mac/EnvironmentLogger/2016-04-07/2016-04-07_12-00-07_enviromentlogger.json ~/rgr`

It will also be called in hyperspectral_workflow.sh

* hyperspectral_metadata.py

In terminal, use the following command line:

`python ${HOME}/terraref/computing-pipeline/scripts/hyperspectral/hyperspectral_metadata.py ${DATA}/terraref/test_metadata.json ${DATA}/terraref/data`

It will also be called in hyperspectral_workflow.sh

* hyperspectral_workflow.sh

In terminal, use the following command line (assume the hyperspectral files are save in projects/arpae/terraref/raw_data/ua-mac/MovingSensor/VNIR/):
`ls -R /projects/arpae/terraref/raw_data/ua-mac/MovingSensor/VNIR/2016-04-07/*/*_raw | hyperspectral_workflow.sh -d 1 -O /gpfs_scratch/arpae/imaging_spectrometer > ~/terraref.out 2>&1 &`








