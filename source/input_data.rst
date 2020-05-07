Installing RainCast input
=============================================

RainCast input format
^^^^^^^^^^^^^^^^^^^^^
RainCast requires two types of input data:

  - Rainfall observations
  - Rainfall forecasts

All the above inputs must be gridded with latitude and longitude information. The observation has to be in MetService CAPPI format (NetCDF), and the forecast can be either in NetCDF (the generic WRF output format) or GRIB

RainCast input location
^^^^^^^^^^^^^^^^^^^^^
Both the observation and forecast have to be presented in the required place:

Forecast dataset
"""""""""""""""""
The forecast dataset must be stored following the structure::
    
    |-- <raincast-top-working-dir>
         |-- download
              |-- nwp
                   |-- wrf
                        |-- <model_name>
                             |-- <analysis_time>
                                  |-- <forecast files>

The forecast filename is dependant on its format: 

  - if the forecast is the generic WRF output (in NetCDF), the filename must follow *wrf_hourly_{model_name}_d02_{valid_time}*, e.g., wrf_hourly_nz4kmN-NCEP_d02_2020-03-18_21:00:00

  - if the forecast is in GRIB format, the filename follows *{model_name}_02_{analysis_time}_{lead_hr}.00.grb*, e.g., nz4kmN-NCEP_02_20030812_014.00.grb
              
Observation dataset
"""""""""""""""""
For now RainCast only supports the MetService CAPPI format. The MS-CAPPI is in NetCDF created by *Py-ART* therefore the user who does not have access to MS-CAPPI should create their own gridded rainfall observation accordingly.

The observation dataset must stored following the structure::

    |-- <raincast-top-working-dir>
         |-- download
              |-- radar
                   |-- nzms
                        |-- <cappi files>

The cappi filename should follow *cappi_reflectivity_<valid_time>.nc*, for example, cappi_reflectivity_202003090300.nc

The CAPPI NetCDF format should follow::



