The aim of this study is to visualize the earthquakes with a minimum magnitude of 2 that occurred in the Marmara region of Turkey in the last 10 years. The source from which I took the earthquake data while carrying out the study was the US Geological Survey (USGS).
Three Python libraries were used in the study. "Requests" to retrieve data from the US Geological Survey (USGS) database via API; "Pandas" to make queries on the data sets we capture, filter, combine, group and analyze the data; "Folium" library was used to visualize the data we processed on an interactive map. Visualizations were done not only within Python using the Folium library, but also outside of Python using Tableau.

At the beginning of the study, various parameters were defined for the API request. The primarily defined parameter is the time interval in which the study will be carried out. The time interval is selected according to the purpose of the study or the desired result. In this study, the last 10-year time period was preferred.

The next parameter is the minimum/maximum size. Since the focal point in this study is relatively large earthquakes, the magnitude was chosen as minimum 2 in order to make the map cleaner and more understandable.

The last parameter is location. This parameter is divided into 3; latitude, longitude and radius. Since the region to be analyzed in this study is the Marmara region, the coordinates of Karacabey district, which is a district relatively close to the midpoint of the Marmara region, were used in terms of latitude and longitude. The most productive radius was determined to be 250 km.

Determining the radius is of great importance, especially in the tabulation process after capturing the data. Choosing a higher radius than necessary will cause the analyst to have to deal with an unnecessary mass of data and therefore cause loss of time. A radius that is lower than necessary will make it impossible to achieve the targeted study result.

After the parameters were prepared, a request was sent to the API. When sending the request, the URL is created with f-string format. The reason for this is that the specified parameters will be placed in the URL, and therefore the URL must be open to dynamic change. Afterwards, the request.get() method was used to send a GET request to the USGS Earthquake API. Afterwards, the response coming through the API was converted to JSON format. The reason for this is to process the data more easily and make it compatible with data structures in Python.

After this stage, list concepts were used to extract only useful data from the earthquake data obtained from the USGS API. For example, a list called places is created. Iterates through each earthquake feature in the 'features' array of the API response (data). For each earthquake feature, its value associated with the 'location' key is extracted under the 'features' dictionary. Ultimately, it represents the place or place where the earthquake occurred. In this way, parameters such as time, place and size determined at the beginning are eliminated from unnecessary data.

A data table was created using the Pandas library. Afterwards, the extracted data was placed in this data table. Thus, before the data was visualized on the map, it was checked on the table whether it was as desired or not. After checking the table, the table was printed in .csv format. The reason for this is that visualization will be done using Tableau other than Python.

First of all, to visualize the earthquake data using the Folium library in Python, the process started by specifying the coordinates on which the map would be centered. These coordinates were used the same as those used to capture earthquake data. After creating a parameter that determines the coordinates, this parameter was entered as location into Folium's map function. Afterwards, a separate parameter was determined for how much to zoom on the map. The zoom amount was determined as 7.5 to include the entire Marmara region.
After the map was created, the coordinate and earthquake magnitude data in the data table were placed into the temperature map function to create a temperature map on the map. In addition, the temperature radius parameter within the function was increased to 20 in order to more clearly indicate how large the earthquakes on the map are with the temperature measurement. Then, the temperature map was added to the map we determined.

A "for" loop was then created and iterated over each row in the DataFrame. Thus, a circular marker was created for each earthquake. The location of the marker is determined according to the Latitude and Longitude values of the earthquake. The radius of the circle is determined by dividing the magnitude of the earthquake (Magnitude) by 2. The color of the circle's outline and fill is set to red. These circles are then added to the map.

![image](https://github.com/YavuzAkbay/earthquake-data-analysis/assets/29518499/757a2da6-f440-4f28-9d60-ebfec9e6e4ef)

After visualization in Python, visualization was made in Tableau with the extracted data table.

![image](https://github.com/YavuzAkbay/earthquake-data-analysis/assets/29518499/7a0ddc33-45e9-4334-8ba8-a07c33e5130f)
