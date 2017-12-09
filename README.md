# Group_5_Project
Group 5 Project Repository

# Project Title - City of Austin 311 Call Analysis

### Team Members: 
Tom Berton, Donna Dietrich, Mike Raigosa, Bopanna Malachira

### Project Description.

  The goal of this project use the 311 call data from the City of Austin over a three-year period from 2014 to 2016 and to determine what are the major concerns of Austinites over three years and within each year, what zip codes have the most 311 calls and determine if there are in any correlations between 311 complaints and other socioeconomic factors by addressing and answering the following questions.
  
### Data retrieval and cleaning.

  In the initial .csv file for the analysis the data span from December 2013 to August 2017. Since 2013 and 2017 were incomplete, we decided to focus only on the years 2014 through 2016.  

### Question 1: How do the number of 311 calls differ yearly and within each year?

  When we analyzed the number of 311 complaints over these three years, we found that the majority of the calls/complaints occurred between April and October regardless of the year. As shown in the figure below, the number of 311 complaints from January - April, and October - December for all three years were equivalent. Interestingly, the number of 311 complaints between May - July of 2015 were greater than the 311 complaints from the same months in 2014 and 2016. Moreover, July of 2016 had the fewer 311 complaints compared to July of 2014 
  <p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/Number_311_calls.png?raw=true "311 Complaints 2014-2016" width="500"/>
  
  ### Question 2: What are the major concerns of citizens of Austin and their community? 
  
  To determine what the major concerns of Austinites over three years we looked at the complaint description and found over 100 different types compliants, which are handled by 20 different departments with the City of Austin government. So, we decided to focus on the distribtution of 311 complaints by department.  We found that the majority of the 311 complaints from 2014 to 2016 where handled by Animal Services, Austin Code, Transportation, Austin Resource Recovery departments and Public Works.

<p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/overviewcodedepartment.png?raw=true "311 Calls by City Services Department" width="500"/>

  Since Austin is considered a pet friendly city it is not surprising to see that the majority of complaints were handled by Animal Services. When we looked at the complaint description for all the complaints handled by Animal Services, we found that loose dogs, assistance from Animal Control, injured/sick made up the majority of these complaints as shown in the figure below.
  <p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/overviewanimalservices.png?raw=true "Animal Services 311 Calls" width="500"/>
</p>
                                                                                                                                                     
                                                                                                                                                     
### Question 3: What is the distribution of 311 complaints in each zip code in Austin?
  
  To address this question we looked at the distribution of the number of 311 complaints by zip code.  We found that the 78745 and 78704 zip codes had the most 311 complaints followed closely by 78702.
  
<p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/Number_311_calls_zip.jpg" 311 Complaints by Zip Code" width="500"/>
</p>

  To get a better visual representation of 311 complaints for each zip code we decided to plot the number of 311 complaints within each zip code on an Austin map. The first approach was use the matplotlib module [Basemap](http://matplotlib.org/basemap/). For this approach, we downloaded the zip codes for the United States form the [US Census Bureau](https://www.census.gov/geo/reference/zctas.html) and imported them into a boundary tool called [BoundingBox](http://boundingbox.klokantech.com/) to specifically select a latitude and longitude coordinate area that includes Travis county. This creates Geojson file for latitude and longitude coordinates that can be used in Basemap. Analysis of our data shows that there are more 311 calls in areas south of the river (blue line). 
  
  <p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/311_call_density_zip.png?raw=true "311 Complaints by Zip Code" width="500"/>
</p>
 
  
  The second approach was to plot the same data above but to represent it as a heat map instead of circle size. For this approach we installed and used [gmaps](https://hpneo.github.io/gmaps/). Gmaps uses JavaScript through an API to map the area of interest and is able to apply a variety of visualization affects, like heat mapping. We used the Texas zip codes from the US Census Bureau and uploaded them to [mapshapper](http://mapshaper.org/).  From mapshapper we focused in on the Travis county area and used the latitude and longitude boundary box to create Geojson file to export. The Geojson file was used in the Jupyter Notebook to map the zip code areas in gmaps with our 311 call data.  As shown in the image below we were able to plot all of the 272,000 311 complaints over three years. Since, we mapped so many 311 complaints it was challenging to determine which zip code have the most complaints based on intensity, however it is clear that the central corridor in Austin has the most 311 complaints.

 
 <p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/Google_heatmap_Austin311.png?raw=true "311 Complaints by Zip Code" width="500"/>
</p>
                                                                                                                                                    

### Question 4: Is there any correlation between the number 311 calls per capita population, income bracket, and crime rate?

To address this question we downloaed population, median household income, crime-rate data from the US Census Bureau. I then used matplotlib to depict the relationship. In order to remove the effect of population on complaint count on the first plot, we decided to plot the 311 complaints/per-capita for each zip code. From the chart below we found that the top-3 zip-codes based on per-capita complaint counts are 78701 (Downtown), 78702 (Central-East Austin) and 78742. 

<p align="left">
  <img src="?raw=true "311 Complaints by Zip Code" width="500"/>
</p>

### Question 5: How do four different neighborhoods in Austin that vary in household income differ in the types of 311 calls?

  Goal was to identify four zip codes with varying median household incomes.  Zip codes selected had the highest calls per capita within each of the four custom groups of zip codes binned by household income. The types of 311 calls were determined by the handling department.  The analysis above identified the five departments that handle the majority of the calls.  Analyzing 311 calls from these five departments and four zip codes reveal the correlation between median household income and the number of 311 calls made. The four selected zip codes illustrate this correlation.
  
<p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/four_zip_codes.png?raw=true "311 Calls in Four Zip Codes" width="500"/>
</p>                                                                                                                                
  
This correlation demands that we assess composition of calls by percentages within each zip code rather than raw counts. The chart below illustrates the varying composition of calls within each zip code. The zipcode with the lowest median household income has the most balanced composition of 311 calls between the five departments.  

<p align="left">
  <img src="https://github.com/mraigosa/Group_5_Project/blob/master/images/Household_Inocme_vs_Department.png?raw=true "Household Income vs Department/Type" width="500"/>
</p>

### The data sets we used are:
- City of Austin, austin_311_service_requests.csv
- The Travis county zip codes from the US Census Bureau.
- Social/Economic census data for Austin, TX by zipcode from the US Census Bureau
- City of Austin Household statistics from the US Census Bureau.
