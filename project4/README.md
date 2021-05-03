# Project 4

Posted: May 3, 2021

Due: May 11, 2021 11:59PM EDT

## Part 1: Getting the Data

Use the following code to install the necessary packages, download the required
data, and perform some minor pre-processing of the DataFrame:

```{python}
!pip install folium
import folium
import requests
import pandas

arrest_table = pandas.read_csv("https://cmsc320.github.io/files/BPD_Arrests.csv")

arrest_table = arrest_table[pandas.notnull(arrest_table["Location 1"])]

arrest_table["lat"], arrest_table["long"] = arrest_table["Location 1"].str.split(",").str
arrest_table["lat"] = arrest_table["lat"].str.replace("(", "").astype(float)
arrest_table["long"] = arrest_table["long"].str.replace(")", "").astype(float)
```

The first few rows should look something like this:

```{python}
arrest_table.head()
```


|     | arrest |  age | race | sex |  arrestDate | arrestTime | arrestLocation  | incidentOffense  | incidentLocation  | charge  | chargeDescription   | district  | post  | neighborhood | Location 1 | lat | long |
| --- | ---    |  --- | ---  | --- |  --- | --- | ---  | ---  | ---  | ---  | ---   | ---  | ---  | ---  | --- |  ---   | --- |
| 1 |11127013.0 | 37 | B | M | 01/01/2011 | 00:01:00  | 000 Wilkens Ave  | 79-Other              | Wilkens Av & S Payson St  | 1 1425 | Reckless Endangerment || Hand Gun Violation | SOUTHERN     | 934.0 | Carrollton Ridge       | (39.2814026274, -76.6483635135) | 39.281403 | -76.648364 |
| 2 |11126887.0 | 46 | B | M | 01/01/2011 | 00:01:00  | 800 Mayfield Ave | Unknown Offense       | NaN                       | NaN    | Unknown Charge                              | NORTHEASTERN | 415.0 | Belair-Edison          | (39.3227699160, -76.5735750473) | 39.322770 | -76.573575 |
| 3 |11126873.0 | 50 | B | M | 01/01/2011 | 00:04:00  | 100 Ashburton St | 79-Other              | 2100 Ashburton St         | 1 1106 | Reg Firearm:Illegal Possession || Hgv       | WESTERN      | 735.0 | Panway/Braddish Avenue | (39.3117196723, -76.6623546313) | 39.311720 | -76.662355 |
| 4 |11126968.0 | 33 | B | M | 01/01/2011 | 00:05:00  | 000 Wilsby Ave   | Unknown Offense       | 1700 Aliceanna St         | NaN    | Unknown Charge                              | NORTHERN     | 525.0 | Pen Lucy               | (39.3382885254, -76.6045667070) | 39.338289 | -76.604567 |


## Part 2: Making a Map

Folium provides a python interface for [leaflet.js](https://leafletjs.com/).
Leaflet.js is a Javascript library for interactive maps, and can be useful to
know on its own. The benefit of using this library via Folium is that Folium
makes it very easy to use from within a Jupyter Notebook and to access your
python data-structures (e.g.  Pandas DataFrames).

The documentation for Folium can be found on its official website:
[https://python-visualization.github.io/folium/](https://python-visualization.github.io/folium/).
You will likely need to consult the documentation in order to complete this
project.

The following code will create a map centered on Baltimore:


```{python}
map_osm = folium.Map(location=[39.29, -76.61], zoom_start=11)
map_osm
```

Note: it is common to see the `osm` suffix because leaflet.js uses
OpenStreetMap.

## Part 3: Combining Parts 1 and 2

Use markers, [as described in the
documentation](https://python-visualization.github.io/folium/quickstart.html#Markers)
to mark information from `arrest_table`. The task for this project is to come
up with a way to differentiate the data marked on the map. If all arrests use
the same marker type, the map will be near meaningless. The columns in
`arrest_table` will be a good first step, but you'll likely want to only
differentiate among a subset of the columns.

## Submission:


Your submission must include the following:


1. the code to carry out each of the steps above

2. output showing the result of your code (in this case the interactive map)

3. a short prose description of your interactive map (i.e., what are you
showing with this data and map). Remember, the writeup you are preparing is
intended to communicate your data analysis effectively.  Thoughtlessly showing
large amounts of output in your writeup defeats that purpose.

This should be submitted on ELMs in the usual way.
