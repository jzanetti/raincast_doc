Setup the working directory
==============================

RainCast reads and writes the data from a certain files hierarchy, 

input data directories:
  - *data_download_radar_loc*: where the MetService CAPPI data are stored (hard coded)
  - *data_download_nwp_loc*: where the NWP forecasts data are stored (hard coded)

Itermediate directories
  - *data_download_regrid_radar_loc*: where the regridded CAPPI data are stored (hard coded)
  - *data_download_regrid_nwp_loc*: where the regridded NWP forecasts data are stored (hard coded)
  - *hist_climatology_dir*: where the NWP skill climatology data are stored (from configuation)

output data directories:
  - *figure_dir*: where the output figures are located (hard coded)
  - *output_dir*: where the output data are located (hard coded)

for super ensmebles:
  - *raincast_ver*: where the runtime RainCast verification data are stored (hard coded, only used in creating super ensembles)
  - *individual_model_output_dir*: where the model name dependant output data are located (hard coded, only used in creating super ensembles)

  
