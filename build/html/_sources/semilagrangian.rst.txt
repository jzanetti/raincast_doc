Semi-Lagrangian extrapolation
==============================


We can run the following codes to get the extrapolated radar image::

	import matplotlib.pyplot as plt
	timestep = 2
	R_out = semilagrangian.extrapolate(
	    R, V, timestep,
	    unit, **extrap_kwargs)

	plt.subplot(121)
	plt.contour(R, colors='r')
	plt.contour(R_out[0, :, :], colors='g')
	plt.contour(R_out[1, :, :], colors='b')

	plt.subplot(122)
	skip = (slice(None, None, 10), slice(None, None, 10))
	u = V[0, :, :]
	v = V[1, :, :]
	plt.quiver(u[skip], v[skip])
	plt.title('Optical Flow')

.. image:: figures/Screenshot_from_2020-04-21_14-33-11.png
   :width: 750

In RainCast, the historical radar data  is extrapolated to the RainCast analysis time::

    for file_index in range(ar_order):
        R_radar[file_index, :, :] = nowcast_extrapolation.run_extrapolation(
            extrapolator_method, R_radar[file_index, :, :], V, extrap_kwargs,
            ar_order=ar_order, file_index=file_index, unit="min")

It is worthwhile to note that:

 - the input *R_radar* (*[time, x, y]*) starts from the goback hours (e.g., 2 hours ago) and ends at the analysis time. 

 - In contrast, the output *R_radar* (*[time, x, y]*) all the data are valid at the same time (the RainCast analysis time), where the data with the 1st time (e.g., *R_radar[0, :, :]*) is the extrapolation from the goback hours (e.g., 2 hours ago), and the one with the 2nd time (e.g., *R_radar[1, :, :]*) is the extrapolation from the second goback hours (e.g., 1 hour ago), and the last one (e.g., *R_radar[2, :, :]*) is the observation (no extrapolation applied).
