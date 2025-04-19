# Food Desert Mobile Market Route Optimization
## For Feeding America's "Oasis" Mobile Farmers Market Initiative

![Food Desert Map](https://www.seriouseats.com/thmb/bjJxZw5PQeMoCn18czKYjqxKWzs=/750x0/filters:no_upscale():max_bytes(150000):strip_icc():format(webp)/__opt__aboutcom__coeus__resources__content_migration__serious_eats__seriouseats.com__images__20110509-food-desert-locator-5daf3632181b44b8ac4f2ff765218776.jpg)

## Project Overview

Food deserts are geographic areas where residents have limited access to affordable, nutritious food options, particularly fresh fruits and vegetables. These areas disproportionately affect low-income communities, leading to increased rates of diet-related health issues. In Texas, particularly in border counties like Hidalgo, the problem is especially acute due to economic disparities, geographic isolation, and infrastructure limitations.

The objective of this project is to optimize mobile farmers market routes in Hidalgo County, Texas, to maximize accessibility to fresh food for residents living in food deserts by December 2025. By utilizing data-driven clustering and route optimization techniques, this project creates efficient service territories and travel routes for a fleet of three mobile markets, allowing Feeding America's "Oasis" Initiative to reach the maximum number of food-insecure residents while minimizing travel time and operational costs.

## Data Dictionary

| Feature | Type | Dataset | Description |
|---------|------|---------|-------------|
| CensusTract | string | FoodDeserts2015.csv | Census tract ID (unique identifier) |
| State | string | FoodDeserts2015.csv | State name |
| County | string | FoodDeserts2015.csv | County name |
| Urban | integer | FoodDeserts2015.csv | Flag indicating urban (1) or rural (0) designation |
| LALOWI1_20 | float | FoodDeserts2015.csv | Count of low-income individuals with low access living more than 1 mile (urban) or 20 miles (rural) from a supermarket |
| LILATracts_1And20 | integer | FoodDeserts2015.csv | Flag indicating if the tract is a Low Income, Low Access area at 1 mile (urban) or 20 miles (rural) threshold (1=yes) |
| GEOID | string | Census Tract Shapefile | Census tract ID for geospatial reference |
| INTPTLAT | string | Census Tract Shapefile | Interior point latitude for the census tract |
| INTPTLON | string | Census Tract Shapefile | Interior point longitude for the census tract |
| geometry | object | Census Tract Shapefile | Polygon geometry representing census tract boundaries |
| LAT | float | Derived | Calculated latitude (float conversion of INTPTLAT) |
| LON | float | Derived | Calculated longitude (float conversion of INTPTLON) |
| cluster | integer | Derived | Assigned food truck/mobile market (0, 1, or 2) |

LILATract_1And10- Foundational definition of a food desert

LILATract_1And20- Rural areas that have more severe food access conditions due to supermarket distance

LILATract_Vehicle- Low-income/low-access area where more than or equal to 100 individuals lack transportation means

TractKids- Number of kids in census tract

TractSeniors- Number of seniors in census tract 

TractHUNV- Number of housing units in the population without a vehicle

TractSNAP- Number of households within populations receiving SNAP

SNAP_percent- Percent of the population receiving SNAP food assistance

Kids_percent- Percent of the population under 17

Seniors_percent- Percent of population aged 65 and up

Houshold_noVehicle_percent- Percent of households in the population without a vehicle

LILA_POP_Density- A metric that compares the LILA population over total land area in miles

INTPTLAT- Latitude 

INTPTLON- Longitude

Coordinates- Longitude, Latitude

Geometry- shape of census tract 

Centroid- Plot of center point within census tract

ALAND/ALAND_miles- Area of land in meters or miles

## Executive Summary

### The Problem
Food deserts affect approximately 19 million Americans, particularly in low-income and rural areas. Hidalgo County, Texas—a border region—has a disproportionate number of food deserts, with over 74,000 low-income residents having limited access to fresh, nutritious food. Traditional grocery stores often avoid these areas due to perceived low profitability, creating a persistent gap in food accessibility.

![figure_1](https://git.generalassemb.ly/algreen59/Project5-FoodDeserts/assets/54579/3b8e7754-eda3-48f9-9da2-0aa9458ec3ed)

### Project Goals
This project aims to design an efficient mobile farmers market system that can reach the maximum number of food desert residents in Hidalgo County while minimizing operational costs and travel time. The specific objectives include:
1. Identifying and mapping all food desert areas in Hidalgo County
2. Clustering these areas into optimal service territories for three mobile markets
3. Determining the most efficient routes for each mobile market, considering time and distance constraints
4. Calculating the potential population impact of the optimized routes

### Methodology
The project utilized a multi-stage analytical approach:
1. **Data Loading and Preprocessing**: U.S. Department of Agriculture Food Desert data and Census Bureau geospatial files were processed to isolate Hidalgo County food desert census tracts.
2. **K-means Clustering**: Geographic coordinates of food desert areas were clustered into three service territories, each assigned to one mobile market.
3. **Hub Selection**: Within each territory, the census tract with the highest population was identified as the starting point for each mobile market.
4. **Distance Calculation**: Haversine distances were computed between all locations within each territory.
5. **Route Optimization**: The Traveling Salesman Problem (TSP) was solved for each territory using Google's OR-Tools library, with a 14-hour workday constraint (assuming 2 hours per stop and 50 mph average travel speed).

### Key Findings
![figure](https://github.com/user-attachments/assets/7db6863b-841e-4493-a1f2-a6737d243ae3)

The analysis generated several significant findings:
- Three distinct service territories emerged: Western, Central/Southern, and Eastern Hidalgo County
- Each mobile market can efficiently serve between 17,000-30,000 residents per day
- The optimal routes require each truck to travel between 11-25 miles and make 6 stops daily
- All routes can be completed within a single 14-hour workday
- The total initiative can potentially serve approximately 75,000 food desert residents
- Approximately 83% of market operation time is spent serving communities rather than driving between locations

### Conclusions
The optimized mobile market system demonstrates significant potential for addressing food desert challenges in Hidalgo County. With just three mobile markets, approximately 75,000 residents living in food deserts can gain access to fresh, nutritious food. The efficient routing means each stop serves an average of about 4,100 people, making this a highly impactful and cost-effective intervention.

The geographic clustering naturally followed community boundaries and transportation corridors, creating compact, efficient service territories. The modest average distance between stops (2.9 miles) confirms that our approach minimizes travel time while maximizing population reach.

### Next Steps
1. **Field Validation**: Conduct on-the-ground assessment of proposed routes, verifying accessibility and potential stop locations
2. **Community Engagement**: Establish relationships with local organizations and community leaders to promote the mobile market program
3. **Inventory Planning**: Determine appropriate product mix based on community preferences and nutritional needs
4. **Pilot Implementation**: Launch a pilot program with one mobile market before scaling to all three
5. **Analytics Refinement**: Incorporate actual road network data and traffic patterns to further optimize routes
6. **Expansion Planning**: Develop a framework for extending the program to other high-need counties in Texas and in other states

While our project currently only provides an optimized route for a smaller portion within Hidalgo County, the algorithm can be applied to other counties and states with minor modifications to the data (replace, US Census Bureau, and USDA Food Atlas data of interest and follow the same general methods outline.) 
Other related connections could be tracking the rate of nutrition-related health conditions (hypertension, diabetes, obesity, etc.) throughout all Census tracts and searching for specific trends in data.

## Repository Contents
- `01_EDA.ipynb`: Exploratory data analysis of food deserts across Texas
- `02_Best_Route_Food_Truck_Hidalgo.ipynb`: Focused analysis and route optimization for Hidalgo County
- `data/`: Directory containing all datasets used in the analysis
  - `FoodDeserts2015.csv`: USDA Food Desert data
  - `2015_CensusTract/`: Census tract shapefile data
- `maps_per_cluster_hidalgo/`: Generated maps for each food truck territory
- `graphs_per_cluster_hidalgo/`: Visualizations of optimized routes

## Technologies Used
- Python 3.11
- Libraries: pandas, numpy, matplotlib, geopandas, scikit-learn, OR-Tools, NetworkX
- Jupyter Notebook for analysis and visualization
- GIS tools for spatial data manipulation

## Acknowledgments
- Data provided by USDA Food Access Research Atlas
- Census tract geographical data from US Census Bureau
- Project completed in partnership with Feeding America's "Oasis" Mobile Farmers Market Initiative

## Citations:
[Geopandas and Contextily assistance](https://medium.com/@jl_ruiz/plot-maps-from-the-us-census-bureau-using-geopandas-and-contextily-in-python-df787647ef77)

[Networkx Documentation](https://networkx.org/documentation/stable/auto_examples/algorithms/index.html)

[Scikit Learn Documentation](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.pairwise.haversine_distances.html)

## Authors
- Marlene Prado
- Andrenique Green
- Omar Rodriguez
- Sobomabo Lawson

## License
This project is licensed under the MIT License - see the LICENSE file for details.
