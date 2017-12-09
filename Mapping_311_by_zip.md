
## Mapping Austin 311 Calls from 2014 - 2016


```python
import os
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.basemap import Basemap
from matplotlib.patches import Polygon
```


```python
#Read the csv file that was downloaded from the City of Austin: "https://data.austintexas.gov/"
Austin_311_df = pd.read_csv('data/All_Austin_311.csv',low_memory=False)

Austin_311_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>incident_zip</th>
      <th>owning_department</th>
      <th>complaint_description</th>
      <th>complaint_type</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>year</th>
      <th>month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>78741</td>
      <td>Animal Services Office</td>
      <td>Loose Dog</td>
      <td>ACLONAG</td>
      <td>30.224549</td>
      <td>-97.690675</td>
      <td>2015</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>78757</td>
      <td>Animal Services Office</td>
      <td>Loose Dog</td>
      <td>ACLONAG</td>
      <td>30.350881</td>
      <td>-97.747492</td>
      <td>2016</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>78744</td>
      <td>Animal Services Office</td>
      <td>Loose Animal (not dog)</td>
      <td>ACLOANIM</td>
      <td>30.199263</td>
      <td>-97.711366</td>
      <td>2014</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>78727</td>
      <td>Austin Code Department</td>
      <td>Austin Code - Request Code Officer</td>
      <td>CODECOMP</td>
      <td>30.425112</td>
      <td>-97.707188</td>
      <td>2014</td>
      <td>11</td>
    </tr>
    <tr>
      <th>4</th>
      <td>78723</td>
      <td>Animal Services Office</td>
      <td>Animal - Proper Care</td>
      <td>ACPROPER</td>
      <td>30.311821</td>
      <td>-97.669302</td>
      <td>2014</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>



### Tom Berton mapped the density of 311 calls in Travis count using the Basemap module in Matplotlib. 


```python
#Use the 'clean_Austin_311_df' and keep the approriate columns for this analysis.

austin_lat_lon = Austin_311_df[["incident_zip", "owning_department","latitude", "longitude"]]

# Change the zip to an integer
austin_lat_lon["incident_zip"] = austin_lat_lon["incident_zip"].astype(int)
austin_lat_lon = austin_lat_lon.rename(columns={"incident_zip":"Zip Code","owning_department":"Number of Complaints",
                                              "latitude": "Lat", "longitude":"Lon"})

# Get the number of complaints from the "Department" and means of the Lat and Lon.
atx_zip_by_latlon = austin_lat_lon.groupby("Zip Code").agg({"Number of Complaints": 'count', "Lat": 'mean', "Lon": 'mean'})
atx_zip_by_latlon.head()
```

    /Users/tom/anaconda/lib/python3.6/site-packages/ipykernel_launcher.py:6: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Complaints</th>
      <th>Lat</th>
      <th>Lon</th>
    </tr>
    <tr>
      <th>Zip Code</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>78610</th>
      <td>31</td>
      <td>30.104558</td>
      <td>-97.776716</td>
    </tr>
    <tr>
      <th>78613</th>
      <td>10</td>
      <td>30.459545</td>
      <td>-97.829108</td>
    </tr>
    <tr>
      <th>78617</th>
      <td>3276</td>
      <td>30.178763</td>
      <td>-97.633562</td>
    </tr>
    <tr>
      <th>78620</th>
      <td>1</td>
      <td>30.284697</td>
      <td>-98.067527</td>
    </tr>
    <tr>
      <th>78621</th>
      <td>1</td>
      <td>30.382937</td>
      <td>-97.392721</td>
    </tr>
  </tbody>
</table>
</div>




```python
total = atx_zip_by_latlon['Number of Complaints'].sum()
print(total)
```

    422827



```python
atx_zip_by_latlon["Coordinates"] = atx_zip_by_latlon[['Lat', 'Lon']].apply(tuple, axis=1)
atx_zip_by_latlon.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Complaints</th>
      <th>Lat</th>
      <th>Lon</th>
      <th>Coordinates</th>
    </tr>
    <tr>
      <th>Zip Code</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>78610</th>
      <td>31</td>
      <td>30.104558</td>
      <td>-97.776716</td>
      <td>(30.1045575026, -97.7767162003)</td>
    </tr>
    <tr>
      <th>78613</th>
      <td>10</td>
      <td>30.459545</td>
      <td>-97.829108</td>
      <td>(30.459545485, -97.829108118)</td>
    </tr>
    <tr>
      <th>78617</th>
      <td>3276</td>
      <td>30.178763</td>
      <td>-97.633562</td>
      <td>(30.1787626893, -97.6335617213)</td>
    </tr>
    <tr>
      <th>78620</th>
      <td>1</td>
      <td>30.284697</td>
      <td>-98.067527</td>
      <td>(30.28469734, -98.06752687)</td>
    </tr>
    <tr>
      <th>78621</th>
      <td>1</td>
      <td>30.382937</td>
      <td>-97.392721</td>
      <td>(30.38293725, -97.39272105)</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Plotting the 311 call density on Travis county zip codes marklines.

fig, ax = plt.subplots(figsize=(10,10))
map = Basemap(resolution='f', # c, l, i, h, f or None
            projection='merc',
            lat_0=30.3, lon_0=-97.8,
            llcrnrlon=-98.2, llcrnrlat=30.02, urcrnrlon=-97.2, urcrnrlat=30.6) 

map.drawmapboundary(fill_color="#FFFFFF")
map.drawrivers(color="#0000FF")

map.readshapefile('USzip_codes/cb_2016_us_zcta510_500k', 'cb_2016_us_zcta510_500k')

def plot_area(Coordinates):
    count = atx_zip_by_latlon.loc[atx_zip_by_latlon.Coordinates == Coordinates]["Number of Complaints"]
    x, y = map(Coordinates[1], Coordinates[0])
    #The count number is too high to plot. So reduce it and plot the area of a circle.
    size = (count/6000) ** 2 + 3.14
    map.plot(x, y, 'o', markersize=size, color='#CC5500', alpha=0.8)


atx_zip_by_latlon.Coordinates.apply(plot_area)
fig1 = plt.gcf()
plt.show()
plt.draw()
fig1.savefig('images/311_call_density_zip.png', dpi=200)
```

    /Users/tom/anaconda/lib/python3.6/site-packages/mpl_toolkits/basemap/__init__.py:3260: MatplotlibDeprecationWarning: The ishold function was deprecated in version 2.0.
      b = ax.ishold()
    /Users/tom/anaconda/lib/python3.6/site-packages/mpl_toolkits/basemap/__init__.py:3269: MatplotlibDeprecationWarning: axes.hold is deprecated.
        See the API Changes document (http://matplotlib.org/api/api_changes.html)
        for more details.
      ax.hold(b)



![png](output_7_1.png)


### Tom Berton mapped the density of 311 calls as a heatmap on a Google map using the 'gmaps' dependency. And an Google Api Key. 


```python
# Import necessary modules
import gmaps
import json
import gmaps.geojson_geometries
import gmaps.datasets
from config import g_key
gmaps.configure(g_key)
```


```python
#Draw the Google heatmap using Lat and Lon from 'atx_zip_by_latlon'
with open("travis.geojson") as f:
    geometry = json.load(f)
    
fig = gmaps.figure()
heatmap_layer = gmaps.heatmap_layer(
    atx_zip_by_latlon[["Lat", "Lon"]], weights=atx_zip_by_latlon["Number of Complaints"],
    max_intensity=50, point_radius=7.5)

geojson_layer = gmaps.geojson_layer(geometry, fill_color=None , fill_opacity=0.0)
fig.add_layer(heatmap_layer)
fig.add_layer(geojson_layer)
fig
```


<p>Failed to display Jupyter Widget of type <code>Figure</code>.</p>
<p>
  If you're reading this message in the Jupyter Notebook or JupyterLab Notebook, it may mean
  that the widgets JavaScript is still loading. If this message persists, it
  likely means that the widgets JavaScript library is either not installed or
  not enabled. See the <a href="https://ipywidgets.readthedocs.io/en/stable/user_install.html">Jupyter
  Widgets Documentation</a> for setup instructions.
</p>
<p>
  If you're reading this message in another frontend (for example, a static
  rendering on GitHub or <a href="https://nbviewer.jupyter.org/">NBViewer</a>),
  it may mean that your frontend doesn't currently support widgets.
</p>




```python
austin_lat_lon['Count'] = (austin_lat_lon['Number of Complaints'] !='').astype(int)
    
austin_lat_lon.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Zip Code</th>
      <th>Number of Complaints</th>
      <th>Lat</th>
      <th>Lon</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>78741</td>
      <td>Animal Services Office</td>
      <td>30.224549</td>
      <td>-97.690675</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>78757</td>
      <td>Animal Services Office</td>
      <td>30.350881</td>
      <td>-97.747492</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>78744</td>
      <td>Animal Services Office</td>
      <td>30.199263</td>
      <td>-97.711366</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>78727</td>
      <td>Austin Code Department</td>
      <td>30.425112</td>
      <td>-97.707188</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>78723</td>
      <td>Animal Services Office</td>
      <td>30.311821</td>
      <td>-97.669302</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Draw the Google heatmap using Lat and Lon from 'atx_zip_by_latlon'
with open("travis.geojson") as f:
    geometry = json.load(f)
    
fig = gmaps.figure()
heatmap_layer = gmaps.heatmap_layer(
    austin_lat_lon[["Lat", "Lon"]], weights=austin_lat_lon["Count"],
    max_intensity=10, point_radius=0.5)

geojson_layer = gmaps.geojson_layer(geometry, fill_color=None , fill_opacity=0.0)
fig.add_layer(heatmap_layer)
fig.add_layer(geojson_layer)
fig
```


<p>Failed to display Jupyter Widget of type <code>Figure</code>.</p>
<p>
  If you're reading this message in the Jupyter Notebook or JupyterLab Notebook, it may mean
  that the widgets JavaScript is still loading. If this message persists, it
  likely means that the widgets JavaScript library is either not installed or
  not enabled. See the <a href="https://ipywidgets.readthedocs.io/en/stable/user_install.html">Jupyter
  Widgets Documentation</a> for setup instructions.
</p>
<p>
  If you're reading this message in another frontend (for example, a static
  rendering on GitHub or <a href="https://nbviewer.jupyter.org/">NBViewer</a>),
  it may mean that your frontend doesn't currently support widgets.
</p>




```python

```
