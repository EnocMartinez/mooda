# API Reference

This page gives an overview of all public pandas objects, functions and methods. All classes and functions exposed in mooda.* namespace are public.

## WaterFrame

Object to manage data series from marine observatories.

### Constructor(*path*=None)

It creates the instance following variables:

* WaterFrame.data: A pandas DataFrame that contains the measurement values of the time series.
* WaterFrame.metadata: A dictionary that contains the metadata information of the time series.
* WaterFrame.meaning: A dictionary that contains the meaning of the keys of data (i.e. "TEMP": "Sea water temperature").

If there is a path to a NetCDF file, it loads the data from the file.

Parameters | Description | Type
--- | --- | ---
path | Path to a [NetCDF](http://www.oceansites.org/data/) file. | string

### repr

(From mooda >= v0.1.0).

Returns a string containing a printable representation of an object.

Returns | Description | Type
--- | --- | ---
message | Message with basic information about what contains the object. | str

### WaterFrame.from_netcdf(*path*)

Load and decode a dataset from a netcdf file. The compatible netCDF files are from the mooring-buoys of [EMODNET](http://www.emodnet-physics.eu/Map/), [JERICO](http://www.jerico-ri.eu/data-access/), [EMSO](http://emso.eu), and all time series with [NetCDF](http://www.oceansites.org/data/) format.

Parameters | Description | Type
--- | --- | ---
path | Path to a netCDF file or an OpenDAP URL. File-like objects are opened with scipy.io.netcdf (onlynetCDF3 supported). | string or obj

Returns | Description | Type
--- | --- | ---
True/False | It indicates if the procedure was successful. | bool

### WaterFrame.to_netcdf(*path*)

Write WaterFrame contents to a netCDF3-64bits file.

Parameters | Description | Type
--- | --- | ---
path | Path of the netCDF file. | str

Returns | Description | Type
--- | --- | ---
True/False | It indicates if the procedure was successful. | bool

### WaterFrame.from_pickle(*path*)

Load and decode a WaterFrame object from a pickle file.

Parameters | Description | Type
--- | --- | ---
path | Path of the pickle file. | string

Returns | Description | Type
--- | --- | ---
True/False | It indicates if the procedure was successful. | bool

### WaterFrame.to_pickle(*path*)

It creates a pickle (serialize) file of the WaterFrame.

Parameters | Description | Type
--- | --- | ---
path | Path to save the pickle file. | string

Returns | Description | Type
--- | --- | ---
True | Operation successfully completed. | bool

### WaterFrame.to_csv(*path*)

It saves the WaterFrame data and metadata into a CSV file.

Parameters | Description | Type
--- | --- | ---
path | Path to save the CSV file. | string

Parameters | Description | Type
--- | --- | ---
True/False | It indicates if the process was successful | bool

### WaterFrame.tsplot(*keys*=*None*, *rolling*=*None*, *ax*=*None*, *average_time*=*None*, *secondary_y*=*False*, *color*=*None*)

Plot time series.

Parameters | Description | Type
--- | --- | ---
keys | keys of *self.data* to plot. If None, all parameters of the WaterFrame will be traced. | list of str
rolling | Size of the moving window. It is the number of observations used for calculating the statistic. | int
ax | It is used to add the plot to an input axes object. | matplotlib.axes object
average_time | It calculates an average value of a time interval. You can find all of the resample options [here](http://pandas.pydata.org/pandas-docs/stable/timeseries.html#offset-aliases). | matplotlib.axes object
secondary_y | Plot on the secondary y-axis. | bool
color | Color of the traces. Any matplotlib color can be possible. | str or list of str

Returns | Description | Type
--- | --- | ---
ax | New axes of the plot. | matplotlib.AxesSubplot

### WaterFrame.barplot(*key*, *ax*=*None*, *average_time*=*None*)

Bar plot of time series.

Parameters | Description | Type
--- | --- | ---
key | keys of *self.data* to plot. | list of str
ax | It is used to add the plot to an input axes object. | matplotlib.axes object
average_time | It calculates an average value of a time interval. You can find all of the resample options [here](http://pandas.pydata.org/pandas-docs/stable/timeseries.html#offset-aliases). | matplotlib.axes object

Returns | Description | Type
--- | --- | ---
ax | New axes of the plot. | matplotlib.AxesSubplot

### WaterFrame.scatter_matrix(*keys*, *ax*=*None*)

Draw a matrix of scatter plots.

Parameters | Description | Type
--- | --- | ---
key | keys of self.data to plot. | list of str
ax | It is used to add the plot to an input axes object. | matplotlib.axes

Keys must contain different words. Example:

* keys = ['VAVH', 'VCMX'] is ok.
* keys = ['VAVH', 'VAVH'] is not ok.

Returns | Description | Type
--- | --- | ---
ax | New axes of the plot. | matplotlib.AxesSubplot

### WaterFrame.qcplot(*key*, *ax*=*None*)

Plot the time series with dots of different colours according to the QC Flag.

Parameters | Description | Type
--- | --- | ---
key | key of self.data to plot. | str
ax | It is used to add the plot to an input axes object. | matplotlib.axes

Returns | Description | Type
--- | --- | ---
ax | New axes of the plot. | matplotlib.AxesSubplot

### WaterFrame.qcbarplot(*key*=*"all"*, *ax*=*None*)

Plot the time series with dots of different colours according to the QC Flag.

Parameters | Description | Type
--- | --- | ---
key | keys of self.data to plot. | str or list of str
ax | It is used to add the plot to an input axes object. | matplotlib.axes

Returns | Description | Type
--- | --- | ---
ax | New axes of the plot. | matplotlib.AxesSubplot

### WaterFrame.spectroplot()

It plots the spectrometer of the acoustic data.

Returns | Description | Type
--- | --- | ---
ax | New axes of the plot. | matplotlib.AxesSubplot

### WaterFrame.profileplot(*parameter_y*, *parameter_x*=*None*, *ax*=*None*)

It creates a graph a profile plot. Y-axes suppose to be a depth related parameter.

Parameters | Description | Type
--- | --- | ---
parameter_y | Y-axes parameter. | str
parameters_x | X-axes parameter. | list of str, str
ax | It is used to add the plot to an input axes object. | matplotlib.axes

Returns | Description | Type
--- | --- | ---
ax_out | New axes of the plot. | matplotlib.AxesSubplot

### WaterFrame.hist(*parameter*=*None*, *mean_line*=*False*, *\*\*kwds*)

Make a histogram of the WaterFrame's.

A histogram is a representation of the distribution of data. This function calls DataFrame.hist(), on each parameter of the WaterFrame, resulting in one histogram per parameter.

Parameters | Description | Type
--- | --- | ---
parameter | keys of self.data to plot. If parameter=None, it will plot all
                parameters. | str or list of str or None
mean_line | It draws a line representing the average of the dataset. | bool
**kwds | All other plotting keyword arguments to be passed to DataFrame.hist(). <https://pandas.pydata.org/pandas-docs/version/0.23/generated/pandas.DataFrame.hist.html> | --

Returns | Description | Type
--- | --- | ---
axes | New axes of the plot. | matplotlib.AxesSubplot or numpy.ndarray of them

### WaterFrame.spike_test(*key*, *window*=*0*, *threshold*=*3*, *flag*=*4*)

It detects spikes in a time series.

Parameters | Description | Type
--- | --- | ---
key | key of self.data to apply the test. | str
window | Size of the moving window of values to calculate the mean.If it is 0, the function calculates the optimal window. | int
threshold | The z-score at which the algorithm signals. | int
flag | Flag value to write in on the fail values. | int

Returns | Description | Type
--- | --- | ---
outlier_idx | Array with the flags result of the test. | numpy array

### WaterFrame.range_test(*key*, *flag*=*4*)

Check impossible values of a parameter.

Parameters | Description | Type
--- | --- | ---
key | key of self.data to apply the test. | str
flag | Flag value to write in on the fail values. | int

Returns | Description | Type
--- | --- | ---
 True/False | It indicates if the process was successfully. | bool

### WaterFrame.flat_test(*key*, *window*=*3*, *flag*=*4*)

It detects no changes in values of time-series.

Parameters | Description | Type
--- | --- | ---
key | key of self.data to apply the test. | str
window | Size of the moving window of values to calculate the mean.If it is 0, the function calculates the optimal window. | int
flag | Flag value to write in on the fail values. | int

Returns | Description | Type
--- | --- | ---
outlier_idx | Array with the flags result of the test. | numpy array

### WaterFrame.flag2flag(*key*, *original_flag*=*0*, *translated_flag*=*1*)

It changes the flags of the key, from original_flag to translated_flag.

Parameters | Description | Type
--- | --- | ---
key | key of self.data to apply the test. | str
original_flag | Flag number to translate. | int
translated_flag | Translation of the original flag number. | int

### WaterFrame.reset_flag(*key*, *flag*=*0*)

It changes all the flags of the key to the input flag value.

Parameters | Description | Type
--- | --- | ---
key | key of self.data to apply the test. | str
flag | Flag value to write. | int

### WaterFrame.qc(*key*="all", *window*=*3*, *threshold*=*3*, *bad_flag*=*4*, *good_flag*=*1*)

Auto QC process.

Parameters | Description | Type
--- | --- | ---
key | key of self.data to apply the test. If key is all, the test will be applied to all keys | str
window | Size of the moving window of values to calculate the mean. If it is 0, the function calculates the optimal window. | int
threshold | Flag value to write in on the fail values. | int
bad_flag | key of self.data to apply the test. | str
good_flag | Flag value to write in on the good values. | int

### WaterFrame.drop(*keys*, *flags*=*None*)

Remove required keys (and associated QC keys) from self.data requested axis removed.

Parameters | Description | Type
--- | --- | ---
key | keys of self.data to drop. | list of str
flags | Number of flag to drop. It can be None, int or a list of int. If it is None, column will be deleted. | list of int, , int, None

Returns | Description | Type
--- | --- | ---
True/False | It indicates if the process was successfully. | bool

### WaterFrame.rename(*old_name*, *new_name*)

It renames keys of self.data.

Parameters | Description | Type
--- | --- | ---
old_name | key name to change. | str
new_name | New name of the key. | str

### WaterFrame.concat(*waterframe*)

The concat function does all of the heavy lifting of performing concatenation operations along an axis while performing optional set logic (union or intersection) of the indexes on the other axes.

Parameters | Description | Type
--- | --- | ---
waterframe | WaterFrame object to concat to self. | WaterFrame

### WaterFrame.resample(*rule*, *method*=*'mean'*)

Convenience method for frequency conversion and sampling of time series of the WaterFrame object.

Parameters | Description | Type
--- | --- | ---
rule | The offset string or object representing target conversion. You can find all of the resample options [here](http://pandas.pydata.org/pandas-docs/stable/timeseries.html#offset-aliases) | str
method | Save the new value with the mean(), max() or min() function. | "mean", "max" or "min"

Returns | Description | Type
--- | --- | ---
True/False | It indicates if the process was successfully. | bool

### WaterFrame.slice_time(*start*=*None*, *end*=*None*)

Delete data outside the time interval. If start or end is None, the slice will be from the beginning or to the final of the time series.

Parameters | Description | Type
--- | --- | ---
start | Start time interval with format 'YYYYMMDDhhmmss' or timestamp. | str, timestamp
end | Start time interval with format 'YYYYMMDDhhmmss' or timestamp. | str, timestamp

### WaterFrame.clear()

It delete all data and metadata of the waterframe.

### WaterFrame.memory_usage()

Memory usage of the WaterFrame.

Returns | Description | Type
--- | --- | ---
size | Number of bytes in use. | int

### WaterFrame.parameters()

It return the parameter list used in this WaterFrame. The parameters are the keys of self.data without "_QC".

Returns | Description | Type
--- | --- | ---
parameter_list | Parameters used in the WaterFrame. | list of str

### WaterFrame.use_only(*parameters*=None, *flags*=*None*, *dropnan*=*False*)

Drop all parameters not presented in the input list with QC flags different than given in the input flags.

Parameters | Description | Type
--- | --- | ---
parameters | Parameters to save in the WaterFrame. If parameters is None, all parameters will be used.| list of str, str, None
flags | QC Flag of the parameter to save. | list of int, int, None
dropnan | Drop all lines of self.data that contain a nan in any of their columns. | Bool

### WaterFrame.corr(*parameter1*, *parameter2*, *method='pearson'*, *min_periods=1*)

Compute pairwise correlation of data columns of parameter1 and parameter2, excluding NA/null values.

Parameters | Description | Type
--- | --- | ---
parameter1 | Key name of the column 1 to correlate. | str
parameter2 | Key name of the column 2 to correlate. | str
method | {‘pearson’, ‘kendall’, ‘spearman’} pearson : standard correlation coefficient, kendall : Kendall Tau correlation coefficient, spearman : Spearman rank correlation | str, optional
min_periods | Minimum number of observations required per pair of columns to have a valid result. Currently only available for pearson and spearman correlation. | int, optional

Returns | Description | Type
--- | --- | ---
correlation_number | correlation coefficient | float

### WaterFrame.max_diff(*parameter1*, *parameter2*)

Calculation the maximum difference between values of two parameters.

Parameters | Description | Type
--- | --- | ---
parameter1 | Key name of the column 1 to calculate the difference. | str
parameter2 | Key name of the column 2 to calculate the difference. | str

Returns | Description | Type
--- | --- | ---
(where, value) | The position (index) and value of the maximum difference. | (Pandas DataFrame Index, float)

### WaterFrame.max(*parameter*)

It returns the max value of a parameter.

Parameters | Description | Type
--- | --- | ---
parameter | Key name of the column to find the maximum value. | str

Returns | Description | Type
--- | --- | ---
(where, value) | The position (index) and value of the maximum value. | (Pandas DataFrame Index, float)

### WaterFrame.min(*parameter*)

It returns the min value of a parameter.

Parameters | Description | Type
--- | --- | ---
parameter | Key name of the column to find the minimum value. | str

Returns | Description | Type
--- | --- | ---
(where, value) | The position (index) and value of the minimum value. | (Pandas DataFrame Index, float)

### WaterFrame.mean(*parameter*)

It returns the mean value of a parameter.

Parameters | Description | Type
--- | --- | ---
parameter | Key name of the column to calculate the value. | str

Returns | Description | Type
--- | --- | ---
mean | The mean value. | float

## PlotMap

 It contains functions related to the management of maps. It creates an instance variable called 'm' that is a Basemap object. We are going to use and modify 'm' in all functions.

### PlotMap._\_init_\_()

    It creates the instance variable *m*. *m* id s Basemap object.

### PlotMap.map_world(*res*=*'l'*)

It creates a map of the world and saves into 'm'.

Parameters | Description | Type
--- | --- | ---
res | Resolution of boundary database to use. Can be c (crude), l (low), i (intermediate), h (high), f (full) or None. If None,  no boundary data will be read in (and class methods such as draw coastlines will raise an if invoked). Higher res datasets are much slower to draw. | str, 'l', 'i', 'h', 'f'

### PlotMap.map_mediterranean(*res*=*'l'*)

It creates a map of the Mediterranean.

Parameters | Description | Type
--- | --- | ---
res | Resolution of boundary database to use. Can be c (crude), l (low), i (intermediate), h (high), f (full) or None. If None, no boundary data will be read in (and class methods such as draw coastlines will raise an if invoked). Higher res datasets are much slower to draw. | str, 'l', 'i', 'h', 'f'

### PlotMap.add_point(*lon*, *lat*, *dot_color*=*'blue'*, *label*=*None*, *label_color*=*Green*)

It adds points to the map.

Parameters | Description | Type
--- | --- | ---
lon | Longitude. | float
lat | Latitude. | float
label_color | Color of the point. | str
label | Text to write in the point. | str
label_color | Color of the label. | str

## access.EGIM

Class to download [EGIM](http://www.emsodev.eu) data using the EMSODEV DMP API.

### EGIM.\_\_init\_\_()

It creates the instance variables login and password to use the DMP API.

Parameters | Description | Type
--- | --- | ---
login | Login of the EMSODEV DMP API. | str
password | Password of the EMSODEV DMP API. | str

### EGIM.observatories()

It represents the EGIM observatories accessible through the EMSODEV DMP API.

Returns | Description | Type
--- | --- | ---
(statusCode, observatoryList) | ([Status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), list with names of observatories) | (int, list of str)

### EGIM.instruments(*observatory*)

It represents the instruments deployed in an EGIM observatory.

Parameters | Description | Type
--- | --- | ---
observatory | EGIM observatory name. | str

Returns | Description | Type
--- | --- | ---
(statusCode, instrumentList) | ([Status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), list with dictionaries of available instruments) | (int, list of dict{"name": "string", "sensorLongName": "string", "sensorType": "string", "sn": "string"})

### EGIM.metadata(*observatory*, *instrument*)

Get EGIM observatory instrument resource.

Parameters | Description | Type
--- | --- | ---
observatory | EGIM observatory name. | str
instrument | Instrument name. | str

Returns | Description | Type
--- | --- | ---
(statusCode, metadataList) | ([Status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), list with dictionaries of metadata) | (int, list of dict{{"instrumentName": "string", "metadataList": [{"metadata": "string","validityDate": "string"}]}})

### EGIM.parameters(*observatory*, *instrument*)

Get the list of EGIM parameters for a specific EGIM instrument of an EGIM Observatory.

Parameters | Description | Type
--- | --- | ---
observatory | EGIM observatory name. | str
instrument | Instrument name. | str

Returns | Description | Type
--- | --- | ---
(statusCode, parameterList) | ([Status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), list of dict of parameters) | (int, list of dict{"name": "string", "uom": "string"})

### EGIM.observation(*observatory*, *instrument*, *parameter*, *startDate*=*None*, *endDate*=*None*, *limit*=*None*)

Gets the time-series of a specific EGIM parameter in a certain  time range or  the last X (limit) values for an EGIM instrument of an EGIM observatory.

Parameters | Description | Type
--- | --- | ---
observatory | EGIM observatory name. | str
instrument | Instrument name. | str
parameter | Parameter name. | str
startDate | Beginning date for the time series range. The date format is dd/MM/yyyy. If the start time is not supplied, we are going to use 'limit'. | str
endDate | End date for the time series range. The date format is dd/MM/yyyy. If the end time is not supplied, the current time will be used. | str
limit | The last x-measurements. | str

Returns | Description | Type
--- | --- | ---
(statusCode, data) | ([Status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), list of DataFrame) | (int, list with dict of parameters)

### EGIM.acoustic_date(*observatory*, *instrument*)

Gets the date list of available acoustic files observed by a specific EGIM instrument of an EGIM Observatory.

Parameters | Description | Type
--- | --- | ---
observatory | EGIM observatory name. | str
instrument | Instrument name. | str

Returns | Description | Type
--- | --- | ---
(statusCode, data) | ([Status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), list with dict of dates) | (int, list of dict{})

### EGIM.acoustic_observation(*observatory*, *instrument*, *date*, *hour_minute*)

Gets an Acoustic file for a specific EGIM instrument of an EGIM Observatory.

Parameters | Description | Type
--- | --- | ---
observatory | EGIM observatory name. | str
instrument | Instrument name. | str
date | Date of Acoustic file. The date format is dd/MM/yyyy. | str
hour_minute | Hour and Minute of an Acoustic file. The Hour Minute format is HHMM. | str

Returns | Description | Type
--- | --- | ---
(statusCode, text) | ([Status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), text of the acoustic file) | (int, str)

### EGIM.to_waterframe(*data*, *metadata*)

It creates a WaterFrame object from the input variables.

Parameters | Description | Type
--- | --- | ---
data | Pandas DataFrame with data without WaterFrame format. | Pandas DataFrame
metadata | Dictionary with metadata information. | dict

Returns | Description | Type
--- | --- | ---
wf |  Data and metadata formated in a WaterFrame Object. | WaterFrame

### EGIM.to_netcdf(*observatory*, *instrument*, *data*, *path*, *qc_tests*=*True*, *only_qc*=*True*)

From mooda v0.2.0.

It creates a netCDF file following the [OceanSites](http://archimer.ifremer.fr/doc/00250/36149/34703.pdf) standard.

Parameters | Description | Type
--- | --- | ---
observatory | EGIM observatory name. | str
instrument | Instrument name. | str
data | Data to be saved into a netCDF file. | Pandas dataframe, WaterFrame
path | Path to save the netCDF file | str
qc_tests | It indicates if QC test should be passed. | bool
only_qc | It indicates to save only values with QC = 1. | bool

### EGIM.to_csv(*observatory*, *data*, *path*, *qc_tests*=*True*, *only_qc*=*True*)

From mooda v0.2.0.

It creates a csv file following the OceanSites standard.

Parameters | Description | Type
--- | --- | ---
observatory | EGIM observatory name. | str
data | Data to be saved into a netCDF file. | Pandas dataframe, WaterFrame
path | Path to save the csv file | str
qc_tests | It indicates if QC test should be passed. | bool
only_qc | It indicates to save only values with QC = 1. | bool
