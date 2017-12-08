# Group_5_Project
Group 5 Project Repository

# Project Title - City of Austin 311 Call Analysis

### Team Members: 
Tom Berton, Donna Dietrich, Mike Raigosa, Bopanna Malachira

### Project Description.

  The goal of this project was to analyze 311 calls in the City of Austin over a three-year period from 2014 – 2017 and to determine what are the major concerns of citizens of Austin, how do the number of 311 calls differ over 3 years and within each year, what Austin zip codes have the most / least 311 calls and is there in any correlation of 311 calls with other socioeconomic factors and crime by addressing and answering the following questions.

### Question 1: How do the number of 311 calls differ yearly and within each year?

  We were fortunate to have such a large data set for 311 calls. We found that the initial .csv file had data from December 2013 - August 2017. Since 2013 and 2017 were incomplete, we decided to focus only on the years 2014 - 2016.  
  
  When we analyzed the number of 311 complaints over these three years, we found that the majority of the calls/complaints occurred between April and October. As shown in the figure below, the number of 311 complaints from January - April, and October - December for all three years were equivalent. Interestingly, the number of 311 complaints between May - July of 2015 were greater than the 311 complaints from the same months in 2014 and 2016. Moreover, July of 2016 had the fewer 311 complaints compared to July of 2014 
  <p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/Number_311_calls.png?raw=true "311 Complaints 2014-2016" width="500"/>
  
  ### Question 2: What are the major concerns of citizens of Austin and their community? 
  
  All 311 calls are handled by different departments with the City of Austin government. As shown in the figure below, we analyzed which departments handled the most complaints. 
  We found that the majority of the 311 complaints from 2014-2016 where handled by Animal Services, Austin Code, Transportation, Austin Resource Recovery departments and Public Works.

<p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/overviewcodedepartment.png?raw=true "311 Calls by City Services Department" width="500"/>

  Since Austin is considered a pet friendly city it is not surprising to see that the majority of complaints were handled by Animal Services. When we looked at the complaint description for all the complaints handled by Animal Services, we found that loose dogs, assistance from Animal Control, injured/sick made up the majority of these complaints as shown in the figure below.
  <p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/overviewanimalservices.png?raw=true "Animal Services 311 Calls" width="500"/>
</p>
                                                                                                                                                     
                                                                                                                                                     
### Question 3: What is the distribution of 311 complaints in each zip code in Austin?
  
  Breaking down the distribution of the number of 311 complaints by zip code, we found that the 78745 and 78704 zip codes had the most 311 complaints followed closely by 78702.
  
<p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/Number_311_calls_zip.jpg" 311 Complaints by Zip Code" width="500"/>
</p>

  To get a better visual representation of 311 complaints we decided to plot the number of 311 complaints for each zip code on an Austin map. The first approach was use a matplotlib module Basemap. The documentation for Basemap can be found [here](http://matplotlib.org/basemap/). For this approach, we downloaded the zip codes for the United States and then used a boundary tool called [BoundingBox](http://boundingbox.klokantech.com/) to select the latitude and longitude coordinates of Travis county to use with Basemap. Finally, as shown in the figure below, we plotted the number of 311 calls in the zip codes as the area of a circle, where the size of the circle increases as the number of 311 calls increases. . 
  
  <p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/311_call_density_zip.png?raw=true "311 Complaints by Zip Code" width="500"/>
</p>
 
  
  Although visual was a nice representation we wanted to get a heat map of the 311 complaints for Travis county. To do this we used [gmaps](https://hpneo.github.io/gmaps/), which needs to be downloaded and installed in the Anaconda folder. Gmaps uses JavaScript through an API to map the area of interest and be able to apply a variety of visualization affects, like heat mapping.
  
  For this approach, we had to get the latitude and longitude of the area we wished to map. We downloaded the Texas zip codes from the US Census Bureau and then uploaded them to [mapshapper](http://mapshaper.org/) then narrowed in on the Travis county area and copied the latitude and longitude boundary box and use mapshapper to create Geojson file to export. We used this Geojson file to set our area which we wanted to map in gmaps and plot our data.  As shown in the image below we were able to all 272,000 311 complaints for over three years. Since, we map so many 311 complaints it’s difficult to see which zip code areas have the most. But it is clear that the central corridor has the most 311 complaints.

 
 <p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/Google_heatmap_Austin311.png?raw=true "311 Complaints by Zip Code" width="500"/>
</p>
                                                                                                                                                    

### Question 4: Is there any correlation between the number 311 calls and income, population or the number of crimes by zip code?



### Question 5: How do four different neighborhoods in Austin that vary in household income differ in the types of 311 complaints?

  Goal was to identify four zip codes with varying median household income.  Zip codes selected had the highest calls per capita within each of the four custom groups of zip codes binned by household income. The types of 311 calls were determined by the handling department.  The analysis above identified the five departments that handle the majority of the calls.  Analyzing 311 calls from these five departments and four zip codes reveals the correlation between median household income and the number of 311 calls made.
  
<p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/four_zip_codes.png?raw=true "311 Calls in Four Zip Codes" width="500"/>
</p>
                                                                                                                                                
  
  
After identifying four varying zip codes by household income and five highest department/types, we analyzed the composition of calls within each zip code.
<p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/Household_Inocme_vs_Department.png?raw=true "Household Income vs Department/Type" width="500"/>
</p>

### The data sets we used are:
- City of Austin, austin_311_service_requests.csv
- The Travis county zip codes from the US Census Bureau.
- Social/Economic census data for Austin, TX by zipcode from the US Census Bureau
- City of Austin Household statistics from the US Census Bureau.
