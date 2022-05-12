Hello! Welcome to my spatial python tool for exploring land use regressions and visualizing principal component analyses (PCAs). I'd like to emphasize that this is an exploratory process, so while there are multiple functions in this tool, they are not neccessarily all meant to be run in order or at all. Instead, you should use these tools to visualize your data and determine multivariate regressions. 

When you open LUR.ipynb, you'll notice that the second cell is comprised entirely of functions. I also define these same functions within the code in examples of how to use the code, however if your using these functions on fresh data you should copy that second cell and utilize the functions as you see fit. 


Python version - 3.7.9

Packages needed:
  - pandas
  - geopandas
  - sklearn
  - numpy
  - matplotlib
  - scipy
  - statsmodels
  - rasterio 
  - rasterstats
  - folium
  
Functions:

split_col:
  usage - split a dataframe based on userdefined observations
  inputs:
    ctrl_list - a list of strings corresponding to the index values to split the data by
    data - the full dataframe you wish to split
  outputs:
    ctrl_data - the data that has the indexes the user specifies
    rest_data - the rest of the data


sub_ctrl:
  usage - subtracts a statistic determined by a dataframe from other observations. Likely from a control dataset and actual data
  inputs:
    controls - the control dataframe (must have the same columns as data)
    data - the data the control statistic will be taken from 
    stat - the statistic performed on the controls variable (count, mean, std, min, 25%, 50%, 75% max)
    


my_recode:
  usage - recodes a dataset based on a user defined limit into 1s and 0s
  input:
    chemical - the variable to be recoded
    lim - the limit by which the chemical variable will be compared against
  outputs:
    either a 1 or a 0 depending on the relation of chemical to the limit



normalizeme:
  usage - normalize a dataframe (likely for input into a PCA)
  input:
    df - the dataframe to be normalized
  outputs:
    a normalized list of data. Also prints the mean (should be 0) and the standard deviation (should be 1)
   


init_pca:
  usage - intializes and runs a PCA on normalized data
  input:
    components - the number of components the user wants defined in the PCA
    data - the normalized data the PCA will be run using
  output:
    p_Cdf - a dataframe holding the results of the PCA 
    init - the initial PCA 



scatter_pca:
  usage - creates a scatter plot of sample data's loadings on user defined Dimensions from a PCA
  input:
    dimn - one of the dimensions to be plotted
    dim2 - the other dimension to be plotted
    iloc1 - the numerical index location of dimn
    iloc2 - the numerical index location of dim2
    pca_df - the dataframe holding the PCA results
    indexer - the original dataframe used to create the PCA (before the normalization function)
    title - user defined title
   outputs:
    a scatter plot of each sample points loadings over the user defined dimensions. Labels points with each sample index
    
    
  
 plot_eigen:
  usage - Creates a bar chart of each dimensions eigen value ratio (shows the variation explained in the original dataset)
  inputs:
    pca_init - PCA initializer, returned in the init_pca function
    title - title of the bar chart
  outputs:
    a bar chart showing the eigen value ratios, with labels
    
    
    
LU_recode:
  usage - Recodes land use/land cover classification (limited usage, must be modified on a use case basis depending on the land cover types being classified)
  inputs:
    df_series - the data to be reclassified
   outputs:
    the recoded data
    
    
    
    
join_buff:
  usage - creates a buffer from a shapefile with the original shapefile attributes
  inputs:
    buff_size - the desired buffer size, in units based on join_file's crs
    join_file - the file used to create the buffer
    idfield - the primary key from the join_file, used to drop any duplicates in the final spatial join
    
    
    

get_stats:
    usage - gets statistics from a raster using a polygon and assigns a primary key to the stats
  inputs:
    buffer - the polygon used to mask the raster
    raster - the raster to grab statistics from
    idfield - the polygon's primary key
  outputs:
    dataframe with statistics and each zone's primary key
   
   
 
 
get_ptst:
    usage - get value from a raster at a specific point and assign the original points primary key
  inputs:
    points - point shapefile 
    raster - raster to get stats from
    idfield - point shapefile primary key
    fieldname - raster value field name
  outputs:
    datafrmae with raster value and primary key
    
    
  
 
 drop_corr:
  usage - drops correlation below correlation limit (note, drops all relationship, better methodology may be to examine correlation in a correlation matrix)
  inputs:
    data - dataframe to examine cross correlation
    corr_lim - correlation limit at which to drop variables
  outputs:
    printed list of variables dropped and dataframe without dropped variables
    
    
    

get_corr:
  usage - gets correlation between several independent variables and a dependent variable in multiple bivariate regressions
  inputs:
    df - dataframe with the dependent variable
    df1 - dataframe with independent variables
    depend - column name for dependent variable
  outputs:
    dataframe showing the results of the regressions
    
    
    

step_reg_back:
  usage - stepwise linear regression, backwards. starts with full regression and modifies model until it cannot be improved further
  inputs:
    y - dependent variable series
    x - independent varaible series (must have constant value in dataframe)
    plim - p-value limit, defaults at 0.05
  outputs:
    regression with refined formula. 
    
