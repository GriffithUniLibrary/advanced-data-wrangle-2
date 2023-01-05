---
title: Find
nav: true
---
# Find a suitable variable

--------

The aim of this lesson is to enhance the  `QldShark_2017_Clean_v2` dataset by adding new variables, to explore if rainfall occurred on the days that sharks were captured and to add scientific names to the common shark names, protection status and distribution values to the dataset where possible. 

The Bureau of Meterology rainfall dataset for the Gold Coast Seaway `BOM_GCS_Rain_2017.csv` and the `NESP_SharkSpeciesList.csv` datasets could be a good matches. We will only match Gold Coast shark captures with the rainfall data in this lesson. It is possible to find and download the other relevant QLD coastal rainfall datasets from BOM.

Let's add the rainfall variable first.  We need to identify a common variable in each of the datasets that we can match on.  A key variable.  To do this we need to explore both datasets to see if a key or very similar variable is available that we can work with. 

Let's open another instance of OpenRefine to explore the  `BOM_GCS_Rain_2017.csv` dataset first.  

{% capture text %}
- Select the `Open` button in the top right hand corner of OpenRefine to open a new instance of the software in your browser.  
- Create a new project using  `BOM_GCS_Rain_2017.csv`  dataset
- Name it  `BOM_GCS_Rain_2017`
- Look at both datasets, what variables do they have in common?
  - `Date`  column in  `QldShark_2017_Clean_v2`
  - `Year` ,  `Month` and  `Day` columns in  `BOM_GCS_Rain_2017`.
 
These could be used as a key to match on. The unique key will be in the `BOM_GCS_Rain_2017` dataset as each date only occurs once and can be matched and added to the same date as many times as appropriate in the `QLDShark_2017_Clean_v2` data.

At present the date is represented in three columns, `Year`, `Month` and `Day`. We need to combine (concatinate) the values of the columns into one column, and add a specific string to the new column’s values, such as a common separator, that matches the format in `QLDShark_2017_Clean_v2`.

- Go to `BOM_GCS_Rain_2017` OpenRefine project
- At  `Year`  column select  `Edit column > join columns`
- Tick  `Year` ,  `Month`  and  `Day`  boxes
- add the separator  `-` (dash) between the content of each column so it will match the date format in `QldShark_2017_Clean_v2`
- at   `Write result in new column named`  add  `Date`
- OK.

The image below illustrates this step.{% endcapture %}{% include card.md header="Add a new column with values from three columns " text=text %}
{% include figure.html img="OpenRefineJoinColumns.png" alt="Add a column with values from three columns" caption="Joining up columns" width="100%" %}

{% capture text %}
The final step required is to change the underlining text format of the new date variable in `BOM_GCS_Rain_2017` to a standard ISO date format to match the date in `QldShark_2017_Clean_v2`.
- In `BOM_GCS_Rain_2017` OpenRefine project
- Go to `Date` column  `Edit cells > Common transforms > To date`

The cells values are now green and contain values that look like e.g. `2017-01-03T00:00:00Z` in this format yyyy-mm-ddTnn:nn:nnZ.

We want to extract the Rainfall data which is in the column named `Rainfall amount (millimetres)`. It is a long variable name, let's change it.
- Go to `Rainfall amount (millimetres)` column
- select `Edit column > Rename this column`
- add name `Rainfall_mm`
- Ok.{% endcapture %}{% include card.md header="Change variable from text to date format" text=text %}

##### Watch this video to work through the activity 
<div style="padding:75% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/782781381?h=33206ddbfc&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="ConcatentateOpenRefine.mp4"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>

----

<p align="center">
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle-2/content/2-create.html"><-- BACK</a> |
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle-2/content/4-key.html">NEXT --></a>
</p>
