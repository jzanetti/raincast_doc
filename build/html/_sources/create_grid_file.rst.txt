Create RainCast Grid
=============================================

All the inputs of RainCast must be projected onto the same grid. The RainCast software provides a few subroutines to help users to easily get this done.

Using the default grid
^^^^^^^^^^^^^^^^^^^^
The default grid, NZ-STEPS.nc, is provided with the package. This grid covers the most of New Zealand and its surrounding areas.

Creating a new grid
^^^^^^^^^^^^^^^^^^^^
The user can create their own grid easily. One example is to use the script *create_raincast_grids.py*. 

With this example, the user is responsible to get a WRF output file to provide the base projection information

The user is welcomed to create the grid with other methods, the following information is required in the grid::

    dimensions:
	south_north = 510 ;
	west_east = 330 ;
    variables:
	float lat(south_north, west_east) ;
	float lon(south_north, west_east) ;
	float landmask(south_north, west_east) ;
		landmask:_FillValue = -999.f ;

    global attributes:
		:dx = 4000.f ;
		:dy = 4000.f ;
		:cen_lat = -40.62973f ;
		:cen_lon = 173.08f ;
		:truelat1 = -30.f ;
		:truelat2 = -60.f ;
		:moad_cen_lat = -41.00001f ;
		:standard_lon = 167.5f ;
		:proj4 = "+proj=lcc +R=6370000.0 +units=m +lat_0=-41.00000762939453 +lat_1=-30.0 +lat_2=-60.0 +lon_0=167.5 +x_0=387999.33438365784 +y_0=1012002.6447856148 " ;
		:xmin = 0. ;
		:xmax = 1688003.64144781 ;
		:ymin = 0. ;
		:ymax = 2071999.67270328 ;
		:llcrnrlat = -50.2888259887695 ;
		:urcrnrlat = -30.2671699523926 ;
		:llcrnrlon = 161.857543945312 ;
		:urcrnrlon = -178.880249023438 ;
		:projection = "lcc" ;
		:lat_1 = -30. ;
		:lat_2 = -60. ;
		:lat_0 = -41.0000076293945 ;
		:lon_0 = 167.5 ;

  
