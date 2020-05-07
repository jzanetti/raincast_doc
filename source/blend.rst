Blending different forecasting components
=========================================

The forecast is produced by using:
 - NWP forecast

 - Observation (e.g., radar) extrapolation

 - Stochastic noises

The contribution of the individiual element is determined by their skills over spectral space, and they are combined later:: 

    R_total[i, :, :] = 
	R_model_cascades[ensemble_no, i, :, :] * updated_weights['nwp'][t, i, :, :] + \
	R_c_to_use * updated_weights['radar'][t, i, :, :] + \
	R_n_to_use * updated_weights['noise'][t, i, :, :]
                    
    R_total[i, :, :][np.isnan(R_total[i, :, :])] = R_model_cascades[
            ensemble_no, i, :, :][np.isnan(R_total[i, :, :])]

The following figure shows the decomposed from NWP, radar and noises:

.. image:: figures/Screenshot_from_2020-04-22_16-46-00.png
   :width: 700

The weights are also shown here:

.. image:: figures/Screenshot_from_2020-04-22_16-43-16.png
   :width: 700

The final blended forecast is:

.. image:: figures/Screenshot_from_2020-04-22_16-47-36.png
   :width: 300

An example from radar extrapolation, NWP and the blended forecasts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Model forecasts
''''''''''''''''''
The below are the forecasts from NWP forecasts (T+1h to T+4h):

.. image:: figures/model_fcst_202003090600_nz4kmN-NCEP_60.0.png
   :width: 300
.. image:: figures/model_fcst_202003090700_nz4kmN-NCEP_120.0.png
   :width: 300
.. image:: figures/model_fcst_202003090800_nz4kmN-NCEP_180.0.png
   :width: 300
.. image:: figures/model_fcst_202003090900_nz4kmN-NCEP_240.0.png
   :width: 300


Radar extrapolation
''''''''''''''''''''
The below are the radar extrapolations (T+1h to T+4h):

.. image:: figures/radar_ext_202003090600_60.0.png
   :width: 300
.. image:: figures/radar_ext_202003090700_120.0.png
   :width: 300
.. image:: figures/radar_ext_202003090800_180.0.png
   :width: 300
.. image:: figures/radar_ext_202003090900_240.0.png
   :width: 300

The blended forecasts
''''''''''''''''''''''
see the blended forecasts (T+1h to T+4h):

.. image:: figures/raincast25_202003090500_nz4kmN-NCEP_t060_all.png
   :width: 300
.. image:: figures/raincast25_202003090500_nz4kmN-NCEP_t120_all.png
   :width: 300
.. image:: figures/raincast25_202003090500_nz4kmN-NCEP_t180_all.png
   :width: 300
.. image:: figures/raincast25_202003090500_nz4kmN-NCEP_t240_all.png
   :width: 300

All the figures (outputs) can be found here :download:`202003090500.tar.gz <202003090500.tar.gz>`







