# Zillow Project

## Purpose
This project aims to improve our original estimate of the log error by using clustering methodologies.

The customer is the Curie data science team.

## Deliverables
1. Github Repository: [Link](https://github.com/clustering-zillow)
    - Readme (this file)
    - Final Jupyter notebooks walking through the pipeline: Walkthrough_1 & Walkthrough_2
    - .py files with all functions necessary to reproduce the model

## Pipeline

# Planning
- Hypotheses:
    - $H_0$: Engineered features will not reduce logerror
    - $H_a$: Engineered features produced by clustering will reduce logerror

- Predicted Feature (dependent): 'logerror' 

# Acquire Data
- acquire.py has all necessary functions to generate this dataframe from SQL

# Data Preparation
- wrangle_zillow has all functions listed here
    - address missing & null values, data integrity issues, etc.
        - 
    - plot distributions of variables
        - identify outliers
        - decide how/if to scale features
        - find errors or invalid data
    - data dictionary
        1. bathroomcnt = number of bathrooms. Used 'bathroomcnt' instead of 'calculatedbathnbr' or 'fullbathcnt' because the other two fields included nulls, and were essentially the same. Dropped rows with 0 bathrooms, to ensure we were only looking at single residence homes.
        2. bedroomcnt = number of bedrooms. No other fields seemed to contain this info. Dropped rows with 0 bedrooms, to ensure we were only looking at single residence homes.
        3. finishedsquarefeet12 = size of home. 
        4. garagecarcnt = number of car spaces in the garage.
        5. garagetotalsqft = size of garage.
        6. hashottuborspa = boolean field indicating whether or not the property has a hot tub or spa, where null values are 0, and anything else is a 1.
        7. latitude
        8. longitude
        9. lotsizesquarefeet = size of lot. 
        10. poolcnt = number of pools on property
        11. poolsizesum = size of pools
        12. numberofstories = how many stories the home has. Nulls filled with 1, the minimum number.
        13. structuretaxvaluedollarcnt = value of the home itself, as determined by tax adjustor.
        14. taxvaluedollarcnt = value of the propery, home and lot, as determined by tax adjustor.
        15. taxamount = amount of taxes charged by the tax adjustor every year.
        16. taxdelinguencyflag = boolean field indicating whether or not the property is delinquent in paying taxes. 
        17. taxdelinquencyyear = indicates how many years the property has been delinquent in taxes.
        18. logerror = the amount of error generated by zillow's zestimate model.
        19. transactiondate = date field indicating when the property was put on the market.
        20. haversine_distance = calculated haversine distance based on a randomly selected point.
        21. regionid_zip = incorrect zip codes
        22. census_tractandblock = corrected census tract information indicating where the property is located
        23. new_zip = corrected zip codes
        24. median_income = median income for the zip code
        25. county = name of county the property is from. This field came from the fips identifier in the original database. The website we obtained the names of counties from: [link] (https://www.nrcs.usda.gov/wps/portal/nrcs/detail/national/home/?cid=nrcs143_013697)
        26. age = calculated field generated by subtracting 2017 from yearbuilt
        27. tax_rate = calculated field created by dividing the value of the property by the taxamount.
        28. cost_structure_sf = calculated field generated by dividing the structuretaxvaluedollarcnt by finishedsquarefeet12
        29. has_ac = boolean field generated from airconditioningtypeid, where null values are 0, and anything else is a 1.
        30. has_heating = boolean field generated from heatingsystemtypeid, where null values are 0, and anything else is a 1.
        31. has_fire = boolean field generated from fireplacecnt, where null values are 0, and anything else is a 1.
        32. has_garage = boolean field generated from garagecarcnt, where null values are 0, and anything else is a 1.
        33. has_deck = boolean field generated from decktypeid, where null values are 0, and anything else is a 1.
        34. LA = boolean field indicating whether or not the propery is in LA County.
        35. OC = boolean field indicating whether or not the propery is in Orange County.
        36. VC = boolean field indicating whether or not the propery is in Ventura County.
        37. sf_bin = Binned field indicating how many square feet the property has
        38. age_bin = Binned field indicating how old the property is
        39. tax_bin = Binned field indicating what tax rate the property is charged
        40. cluster_fancy = Cluster field generated from the deleted columns 'buildingqualitytypeid', 'roomcnt', 'is_extra'
        41. centroid_buildingqualitytypeid = calculated field indicating the centroids of the clusters in cluster_fancy
        42. centroid_roomcnt = calculated field indicating the centroids of the clusters in cluster_fancy
        43. centroid_is_extra = calculated field indicating the centroids of the clusters in cluster_fancy
        44. cluster_lot = Cluster field generated from the columns 'lotsizesquarefeet', 'landtaxvaluedollarcnt', 'new_zip'
        45. centroid_lotsizesquarefeet = calculated field indicating the centroids of the clusters in cluster_lot
        46. centroid_landtaxvaluedollarcnt = calculated field indicating the centroids of the clusters in cluster_lot
        47. centroid_new_zip = calculated field indicating the centroids of the clusters in cluster_lot
        48. cluster_bins = Cluster field generated from the binned columns 'finishedsquarefeet12', 'age', 'tax_rate'
        49. centroid_finishedsquarefeet12 = calculated field indicating the centroids of the clusters in cluster_bins
        50. centroid_age = calculated field indicating the centroids of the clusters in cluster_bins
        51. centroid_tax_rate = calculated field indicating the centroids of the clusters in cluster_bins
       
# Data Exploration
- Goal: Address questions generated during planning and preparation phases
    - Walkthrough_1 has the finalized version of data exploration

# Feature Selection
- Goal: a dataframe with the features to be used to build the model
    - Walkthrough_1 has the finalized version of feature creation and selection
    - By running Walkthrough_1, a csv file is generated with the finalized version of the dataframe used to create the regression model

# Modeling & Evaluation
- Goal: develop a regression model that performs better than a baseline
    - Walkthrough_2 has the finalized version of model selection and evaluation