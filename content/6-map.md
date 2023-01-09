---
title: Map
nav: true
---
# Map the data
----
#### Create an interactive map of the data using geojson.io

Now for the next exciting step, to map `QldShark_2017_Clean_v2` data via latitude and longitude points.  You can use any spreadsheet tool to prepare a list of coordinate points.   

{% capture text %}
GeoJSON is popular, open format for map data, and works across many tools.  A GitHub repository can automatically display any GeoJSON files in a map view using [Open Street Map](https://www.openstreetmap.org).

GeoJSON data must follow a structured format, and the file name may end with either .geojson or .json. The GeoJSON structured format orders coordinates in longitude-latitude format, the same as X-Y coordinates in mathematics. [(Dougherty, 2017)](https://datavizforall.org/convert-geojson.html)

We will create a map using [geojson.io](http://geojson.io), an open source tool to make, change and publish maps.{% endcapture %}
{% include alert.md text=text color=info %}

{% capture text %}
- Open [http://geojson.io](http://geojson.io)
- Select `Open` > File` 
- Find the  `QldShark_2017_Clean_v2` file in your downloads and `open`
    -  You can alos `Drag the file` onto the map.  
- Zoom into the map to see the coastline of Queensland. 
- Look at features on the right hand window – change  `file view`  from  `JSON`  to  `table`  to see the data structured for the human eye. 
- Click on a  `point`  to show data 
- Untick  `Show style properties`  and save
- Save file as GEOJSON file into downloads.{% endcapture %} {% include card.md header="Map data with GEOJSON" text=text %}

##### See how to map the data with GeoJSON.io in this video.

<div style="padding:66.59% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/787446253?h=4655fa0b1b&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="Map a dataset using geojson.io"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>

----
#### Display the map using Github

We now need a website to display the map.  To do this we are going to upload our geoJSON file to the open source repository [Github](https://github.com/) that can host and share files, code and much more.

Here is an example of an interactive [map](https://github.com/stapletonsl/ClassData2019/blob/master/OzUnis.geojson) created using geoJSON and hosted by Github. Click on the points for information about the locations.

In this next activity learn how Github works and create a repository to host the map via Github's tutorial. The first step is to register for an account.

{% capture text %}
- Go to [https://github.com/](https://github.com/)
- Register for Github account or login if you have one already. 
- Or you can use another hosting service you can embed into.
- Do *Hello World tutorial* [https://guides.github.com/activities/hello-world/](https://guides.github.com/activities/hello-world/)
- Go to your newly created  `Hello World` repository
- Select  `Upload file`
- `Drag and drop`  your newly created  `map.geojson`  file 
- Name it  `Qld_Shark_Captures_2017`
- Congratulations!  You have just published in interactive map with data!{% endcapture %} {% include card.md header="Upload map to Github" text=text %}

See the steps illustrated below.


{% include figure.html img="ADORGithub.JPG" alt="Upload a file to Github repo" caption="Upload a file to Github" width="100%" %}


{% include figure.html img="ADORGitUpload.JPG" alt="Upload a file to Github repo" caption="Select the map.Geojson file" width="100%" %}


**Congratulations! You have finished the Advanced data wrangling lessons!**

----


##### Was this tutorial helpful? Let us know.

{% include button.md text="Complete this quick survey" link= "https://prodsurvey.rcs.griffith.edu.au/prodls200/index.php/589544?FeedbackSource=DataVisBasicsOnlineGitPages&Discipline=Research&Client=&newtest=Y" color="info" %}


----

<p align="center">
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle-2/content/5-tidy.html"><-- BACK</a> |
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle-2/content/7-references.html">References --></a>
</p>
