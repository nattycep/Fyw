Code Version:

Further information about Matlab script to accompany HP paper by Ceperley et al. 

Use NaN for missing values. 


Preparation of Daily Meteo Data:

prepare a csv with 5 columns, with 1 row per day, preferably starting before snow season and spanning (more than) the entire duration of isotope samples. 
This is only for one point, preferably near the outlet where the isotope samples were collected. 
The elevation of this point/station is reported in the Parameter File. 

If temperature data for more than point in the catchment is available, this can be used to inform the value for lapse rate in the parameter file.  If data on whether the precipitation falls as rain or snow is available, this can be used to in form the 2 critical temperatures in the parameter file.  If snow pack depth data is available, this can be used to inform the degree day factor in the parameter file. 
columns:
1) year YYYY
2) month M
3) day D
4) daily precipitation in mm
5) daily mean temperature in deg C


Modification of Parameter File
- add a row to the casestudyparametersV4.csv file for each site with a value for each variable (column) : site name, elevation, lapse rate, degree day factor, critical temperatures (low and high)
- make sure that site name corresponds to calling scripts
- details of units etc. are in casestudyparametersV4.m

Preparation of Isotope Data
Separate Isotope Data into 3 files:  
1) streamisotopes.csv
8 columns: 
year,month,day,hour,minute,second,iso_q,discarge_m3s
- cols 1-6 are the date and time of collection
- col 7 is the isotope value of stream
- col 8 is the discharge at moment of collection
note: elevation is assumed to be always the same, at catchment outlet

 
2) snowisotopes.csv
9 columns: 
Year,Month,Day,Hour,Minute,z_m_asl,iso_snow_dO18,bot_cm,top_cm
- cols 1-5 are the date and time of collection
- col 6 is the elevation of collection
- col 7 is the isotope value of snow
- cols 8 and 9 are the bottom and top of collected layer in cm from surface, surface snow should have a top value of 0

3) rainisotopes.csv
13 columns: 
year,month,day,hour,minute,year,month,day,hour,minute,m_asl,iso_rain,mm
- cols 1-5 are the date and time that collection started
- cols 6-10 are the date and time of collection
- col 11 is the elevation (m. Asl.) of the collection point
- col 12 is the isotope value (per mil)
- col 13 is the depth of the collection (mm - volume divided by bucket/funnel area)



Elevation
- clip a DEM to the watershed area and export the resulting DEM to a csv file with the elevation in m.a.s.l in a single column, note the number of this column and update it in the import data file. 


Output
The code will produce one figure for each site with subplots for each precipitation timeseries option. They will be saved as a .tif, .fig, and .jpg in a new folder "Figures". They will show the Precipitation sine wave, the simulated input, Peq, the stream observations, and convolution input.  
All imported input data will be saved as .mat files in the site folder. A subfolder will be created for all the time series of isotopes in precipitation that were created for the selected options. Intermediary results will be saved as a .mat file in Results according to the site name. Final results will be stored in a file called Table 4, saved both as a .csv and .mat file in the results file.  This table will also be left open in Matlab. These columns correspond to those of Table 4 in the paper. 

