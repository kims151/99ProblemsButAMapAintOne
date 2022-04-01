# MetroSafe Web App  by 99ProblemsButAMapAintOne
The MetroSafe web app is an information tool that public transportation planners can use to build a climate-resilient transportation system across GTHA. The app closely follows Metrolinx’s Corporate Climate Adaptation Plan and aims to fulfil the four key requirements needed to put climate resiliency into practice. The four pillars are as follows: 
1. Awareness education and communication 
2. Assessing vulnerability, risks, and opportunities 
3. Building resiliency across the enterprise 
4. Monitoring and adaptive management 
## Team Members 
* Grace Soo Ah Kim
* Pierce Bourgeois
* Sameer Haqqi
## Mission Statement
MetroSafe is a risk-monitoring app for natural disasters in the GTHA which provides users with an in-depth analysis of the hazards that affect the transportation infrastructure system. This application identifies potential risks and corresponding regions that are most vulnerable to natural disasters and hazards. This tool is a function for the general public, government organizations, and planners to monitor the susceptibility of different regions and ensure resource allocation to protect high-risk infrastructure. MetroSafe contributes toward long-term efficiency by reducing both financial and time-related costs. MetroSafe provides a platform to raise awareness about the various natural disasters impacting the GTHA and helps to educate the key personnel who may use this information to devise solutions to the threats.  

With the use of various data visualization tools, important trends across a given region can be better understood. This information is useful for organizations like Metrolinx to identify future expansion opportunities for transportation infrastructure which identifies the regions facing a lower risk from natural disasters. Combining statistical data with mapping tools, offers opportunity for meaningful statistical analysis. Users can input additional data layers and variables into the app to support their analysis. This promotes research and ensures the application is applicable for a wide range of purposes. The interactive nature of the application allows greater flexibility and control for the user to modify their analysis to their specific needs. 

MetroSafe has been designed as a long-term solution to efficiently manage and monitor transportation infrastructure. This includes measuring the effectiveness of policies and decisions and ensuring there is a common reporting platform.  

With a rapidly growing population and an increasing threat of natural disasters, MetroSafe helps ensure a stable and safer future for Ontarians. 
## How to use the MetroSafe Web App
Upon opening the app, the user is greeted by the About Page, which includes instructions on how to navigate the app and a written legend of the symbols.  

By clicking on an individual station (point feature layer), the user can see a popup with the following information:  
* The weather hazards that impact the station
* Assets that are vulnerable to the specified hazards
* Suscept-score, ranging from 0 to 10. A station with a lower suscept-score is less likely to experience the listed hazards compared to another location with a higher suscept-score.
The query widget, located at the bottom of the app, can be used to highlight stations that are at-risk of a specified weather hazard. The user can export the data onto their device for personal use. The transit layers (station and transit network) are particularly useful for public transportation planners that are in need of climate/weather hazard data. This part of the app directly targets pillars 2, 3, and 4 mentioned above.  

The app also intends to educate the public about climate change, climate projections, and historical flood events in GTHA. This is a tribute to pillar 1 of the Metrolinx report. The projections can be toggled using the layer widget, which is located on the top right corner of the app. The legend of the layers is shown by the legend widget, located adjacent to the layer widget.  

The user can use the bookmark widget, located at the bottom of the app, to learn about major flood events and their impact on the economy, environment, and society.  
##Methodology
MetroSafe utilized reliable climate projection data and unique GIS-based methodlogy to create the layers shown on the map. 
### Creating the layers: Converting climate data 
Climate projection data from Ontario Climate Change Data Portal (CCDP) was downloaded using the following parameters: 
- Variable: Precipitation, Mean Temperature, Max Temperature
- Time Period: 2065 - 2095
- Measurement: Temporal Average
- Average: Summer (for rainfall), Winter (for snowfall)
- Percentile: 90%
Initally, the data is downloaded as .txt. This file was represented onto Excel, and subsequently converted to a table using ArcGIS Pro's Excel to Table Conversion Tool. The table consisted of coordinates and projection values, which were used to create a point shapefile. Then a buffer was created around the points to mimic the data shown on CCDP as accurately as possible. Buffers were created for every climate variable listed above. 
### Creating the layers: Assigning climate data to public transit stations
The public transit stations and network were downloaded from Ontario Government's Open Data Portal. These layers were then uploaded onto ArcGIS Pro. Using the buffer created in the previous step, each station was assigned with climate variables using Spatial Join. Now the stations had all the climate variables within its attribute field. The updated station point shapefile and the network were uploaded onto ArcOnline as web layers. 
### Creating the layers: Climate Projections
The same climate projection data points from the previous step were used to create a raster layer. For this step, IDW (Spatial Analyst) tool was used. The unique parameters are as follows:
- in_point_features: climate projection data
- z_field : magnitude of the projection data (snowfall, rainfall, temp, etc.)
- Extent: GTHA border polygon shp
- Mask: GTHA border polygon shp
The projection layers were then uploaded to ArcOnline. 
### Creating the map
The map for the app was created using ArcOnline. For arcade usage, popup configurations, and symbology, please visit: https://mcmaster.maps.arcgis.com/home/item.html?id=58b42ba54107482483297821739d40c0

##References
1. Canadian Infrastructure Report Card (2016) Informing the Future: The Canadian Infrastructure Report Card, 163
2. Metrolinx (2017). Planning for Resiliency Toward a Corporate Climate Adaptation Plan. https://www.metrolinx.com/en/aboutus/sustainability/Planning_for_Resiliency_2017_EN_final.pdf 
3. Summary of the Flood Resilient Toronto Project (2019). https://www.toronto.ca/wp-content/uploads/2019/05/8e9a-2019-04-25_Flood-Resilient-Report.pdf 

##Data
1. Ontario Government: GO train stations (2016) https://data.ontario.ca/dataset/go-train-stations 
2. Canada Open Government: Flood Disasters in Canada https://data.ontario.ca/dataset/go-train-stations 
3. Ontario Climate Change Data Portal (CCDP) http://ontarioccdp.ca/index_a1b.html?vab=Precip&per=2065.2095&mea=Mean&avg=Annual&pce=p5&lay=110000&pan=111&opc=0.8&zom=8#
4. Statistics Canada: Boundary files https://www12.statcan.gc.ca/census-recensement/2011/geo/bound-limit/bound-limit-2011-eng.cfm 
