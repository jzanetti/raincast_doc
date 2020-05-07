Weights and regression for different RainCast component
========================================================

From here the skills of both NWP and radar extrapolated forecasts are to be regressed towards their climatology, and the weights for them are estimated based on their skills. 

The weight of stochanstic noises is also calculated depending on the skills of NWP and radar.

Weight for NWP forecasts
^^^^^^^^^^^^^^^^^^^^^^^^^

The weights of NWP forecasts (from T0 to T+xhours) are dependant on: 
 - its initial skill and
 - the skill climatology

Climatology
''''''''''''

First we need to find out what is the climatological skill for NWP forecasts. The climatological skill is cascade dependant, and they are produced at every cycle when we generate the initial skill of NWP at T0. For example, the climatology skill of NWP at the scale 2040 km is located in::

    <raincast clim directory>/<model name>/fss_para_2040km_nwp

If the data in the above climotology is less than a certain value, e.g., *min_hist_para_len (default: 12)*, then an initial climatology skill would be applied::

    {'512': 0.999, '216': 0.999, '128': 0.85, '64': 0.75, '32': 0.6, '16': 0.5}

Note that in order to generate less stochastic nosies, the minimum NWP climatology skill is set to 0.5


Temporal regression
'''''''''''''''''''''

The NWP skill is gradually regressed towards its climatology::

    updated_rho['nwp'] = regress_nwp_rho_to_climatology(
	regression_opt['nwp'], 
        filter, rho_model, updated_rho['nwp'], clim_rho['nwp'], 
        tt, timestep, ii, kmperpixel, regression_coefficients)

Also how fast it regresses is dependant on the *regression_coefficients*, the less the value the faster it regresses::

    'nwp': {=
        '512': [160.0, 180.0],
        '216': [125.0, 150.0],
        '128': [100.0, 150.0],
        '64':  [80.0, 120.0],
        '32': [60.0, 90.0],
        '16': [45.0, 70.0],
        },

There is a need to use two parameters to determine the regression rate, that's why we see a list of 2 values above instead of just a single value::

    q = math.exp(-timestep_n*timestep/nwp_regress_coefs[0]) * \
        (2.0 - math.exp(-timestep_n*timestep/nwp_regress_coefs[1]))


Weight for radar extrapolation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The weights of radar forecasts (from T0 to T+xhours) are dependant on: 
 - its initial skill
 - the skill climatology
 - a timing smooth term

Climatology
''''''''''''

The skill of radar extrapolation climatology is not accumulated over time, instead it is a set of predefined parameters depending on the (1) forecast lead time and (2) spatial scales::

    {'[60-120]': 
         {'512.0': [0.3, 0.08], 
          '216.0': [0.2, 0.06], 
          '128.0': [0.11, 0.05], 
          '64.0': [0.2, 0.04], 
          '32.0': [0.1, 0.04], 
          '16.0': [0.05, 0.01]}, 
     '[121-240]': 
         {'512.0': [0.1, 0.05], 
          '216.0': [0.08, 0.04], 
          '128.0': [0.05, 0.02], 
          '64.0': [0.0, 0.0], 
          '32.0': [0.0, 0.0], 
          '16.0': [0.0, 0.0]}, 
     '[241-360]': 
         {'512.0': [0.0, 0.0], 
          '216.0': [0.0, 0.0], 
          '128.0': [0.0, 0.0], 
          '64.0': [0.0, 0.0], 
          '32.0': [0.0, 0.0], 
          '16.0': [0.0, 0.0]}}

There is a program to locate the nearest climatology skill based on the actual lead time and scales of the radar extrapolation::

Temporal regression
'''''''''''''''''''''

The radar skill (obtained from the previous step) then is regressed towards to its target climatology::

    # updated_rho['radar'][0, :, :, :, :] = rho_radar
    updated_rho['radar'][tt, :, :, :, :] = updated_rho['radar'][tt-1, :, :, :, :]
    updated_rho['radar'] = regress_radar_rho_to_climatology(
    	updated_rho['radar'], clim_rho['radar'], tt, 
        timestep, regression_coefficients, jj, ii)

How fast the regression would go is dependant on *regression_coefficients*::

    {'radar': [20, 40]}

Ususally the smaller the coefficients, the faster it would regress.

Temporal smoothing
'''''''''''''''''''''
From the second time step, the skill of radar extrapolation must be smoothed to avoid the abrupt changes during blending::

    if tt > 0:
        updated_rho['radar'] = smooth_radar_rho_over_time(
            updated_rho['radar'], tt, jj, ii)

Note that over the first a few hours, the changes of radar skill may mainly come from the Temporal smoothing instead of the temporal regression

Weight for stochastic noises
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The weights for stochastic noise is dependant on the weights for NWP and radar. The more skills NWP and radar have, the less weight from the noises::

    updated_weights['noise'][tt, ii, :, :] = np.sqrt(
        1.0 - updated_weights['radar'][tt, ii, :, :]**2 - 
        updated_weights['nwp'][tt, ii, :, :]**2)


Outputs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
We get the weights from different forecasting approaches (radar, NWP and stochastic noises) stored in a dict::

    updated_weights = {
        'nwp': [lead_time, cascades, x, y],
        'radar': [lead_time, cascades, x, y]}






