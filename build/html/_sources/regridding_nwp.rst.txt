Regrdding NWP forecasts
========================

Obtain the target latitude and longitude
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

First the target latitude and longtiude are read from the grid file::

    grid_lat, grid_lon = \
        raincast_regrid.read_grid(griddata_meta['grid_path'])

Both the *grid_lat* and *grid_lon* must be two dimension arrays, e.g.,::

	>>> grid_lat
	masked_array(
	  data=[[-50.38595 , -50.387203, -50.38843 , ..., -49.3667  , -49.359264,
		 -49.351803],
		[-50.348835, -50.350094, -50.351322, ..., -49.330265, -49.32283 ,
		 -49.315376],
		[-50.311733, -50.31298 , -50.31421 , ..., -49.29383 , -49.286407,
		 -49.27895 ],
		...,
		[-31.644207, -31.6451  , -31.64598 , ..., -30.915848, -30.910519,
		 -30.905174],
		[-31.60799 , -31.608887, -31.60976 , ..., -30.88012 , -30.874798,
		 -30.869457],
		[-31.571793, -31.572685, -31.573563, ..., -30.844418, -30.839085,
		 -30.833748]],
	  mask=False,
	  fill_value=1e+20,
	  dtype=float32)

NWP forecasts metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The program figures out where to get the NWP forecasts based on this metadata file (at MetService, this file is created when the NWP data is downloaded from AWS), the format of the metadata file is something like::

	0:
	  analysis_time: 2020-03-08_12:00:00
	  model: nz4kmN-NCEP
	  reference_model_path: /home/szhang/eclipse-workspace/raincast_test33_testdata/download/nwp/wrf/nz4kmN-NCEP/2020030812/nz4kmN-NCEP_02_20030812_013.00.grb
	fcst_length: 180
	raincast_time_interval_in_mins: 60
	nwp_start: 2020-03-09_02:00:00
	nwp_end: 2020-03-09_07:00:00
	raincast_analysis_time: 2020-03-09_05:00:00

In the above example, the NWP data valid between 02 UTC and 07 UTC will be used. The analysis time for NWP and RainCast are 12 UTC (-day) and 05 UTC, respectively

Radar data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
We always need to go back at least 2 hours to regrid the radar data since the optical flow requires at least two radar images.


