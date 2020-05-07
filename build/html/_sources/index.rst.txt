.. run_raincast_doc documentation master file, created by
   sphinx-quickstart on Mon Apr 20 15:02:32 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to RainCast documentation
=============================================

**RainCast** is a software producing the rapid refresh seamless rainfall forecasting by combining rainfall observation (extrapolation) and NWP

* Release: 0.0.1

* Date: 2020-04-19

This package is developed by New Zealand Meteorological Service

Questions go to: sijin.zhang@metservice.com

.. topic:: this software is capable of :

    * producing the extrapolration based nowcasts using the STEPS algorithm

    * merging the nowcasts and NWP using the STEPS algorithm

    * blending different NWP sources

    * enhancing the probability forecasts using the neighborhood approach

    * statistically downscaling the precipitation forecasts.


About RainCast
^^^^^^^^^^^^^^^^^^^^
**RainCast** is short for Rainfall foreCasting system, which combines different sources of forecasts together using the advanced spectral analysis technology. This system is designed to be run hourly (or even subhourly) to provide the most updated rainfall information.

* Over a short period (e.g., when the forecast lead time is less than 6 hours), it is expected that the incorporation of observation would improve the skill of forecasts, 

* After the first several hours, most additional values added by RainCast come from the enhanced neighborhood probability approach

* it is always recommended to run RainCast with multiple NWP sources (e.g., HRRR or any global NWPs)

RainCast uses much less computational resources than a full rapid updating forecasting system like HRRR (NOAA) or UKV (UK MetOffice), and only focuses on precipitation. Anyone with a reasonable laptop should be able to use this.

This page is created for any developers/collaborators to get familiar with RainCast

Acknowledgements:
''''''''''''''''''
Australian Bureau of Meteorology, UK MetOffice


Installation
^^^^^^^^^^^^^^^^^^
.. toctree::
  :maxdepth: 1

     dependancies <dependancies.rst>
     conda <conda_env.rst>
     docker <docker_install.rst>


Sample workflow
^^^^^^^^^^^^^^^^^^

Preparation
'''''''''''''''''''
.. toctree::
   :maxdepth: 1

      Creating grid file <create_grid_file.rst>
      Installing input dataset <input_data.rst>
      Setup working directory <working_dir.rst>
      Regriding the inputs <regridding_nwp.rst>
      Locate the input dataset <locate_input.rst>

Radar extrapolation
'''''''''''''''''''''''
.. toctree::
   :maxdepth: 1

      Optical Flow <optical_flow.rst>
      Semi-lagrangian extrapolation <semilagrangian.rst>

Spectral decomposition
'''''''''''''''''''''''
.. toctree::
   :maxdepth: 1

      Decomposition <decomposition.rst>

Correlation at T0
'''''''''''''''''''''''
.. toctree::
   :maxdepth: 1

      Radar correlations <radar_corr_t0.rst>
      NWP correlations <nwp_corr_t0.rst>
      Difference between NWP and radar <diff_radar_nwp_corr_t0.rst>

Climatological regression for NWP and radar forecasts
''''''''''''''''''''''''''''''''''''''''''''''''''''''
.. toctree::
   :maxdepth: 1

      Weights for NWP, radar and nosies <weights.rst>

Noises
'''''''
.. toctree::
   :maxdepth: 1
      
      Create stochastic noise <noise.rst>

Blending forecast
''''''''''''''''''
.. toctree::
   :maxdepth: 1
      
      forecasts blending <blend.rst>

Super Ensemble
''''''''''''''''''
RainCast is able to blend different forecasts together and create the best possible (statistically) combined forecast.

.. toctree::
   :maxdepth: 1
      

      Prepare the inputs for super ensemble <super_prepare.rst>







