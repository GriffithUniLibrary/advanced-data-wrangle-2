---
title: Find
nav: true
---
# Find a suitable variable

--------

The aim of this lesson is to enhance the  `QldShark_2017_Clean_v1.csv` dataset by adding new variables, to explore if rainfall occurred on the days that sharks were captured and to add scientific names to the common shark names where possible. 

The Bureau of Meterology rainfall dataset `BOM_GCS_Rain_2017.csv` and the `NESP_SharkSpeciesList.csv` dataset` could be a good matches.

We need to identify a common value in each of the datasets that we can match on.  A key variable.  To do this we need to explore both datasets to see if a key or very similar variable is available that we can work with. 

Let's open another instance of OpenRefine to explore the  `BOM_GCS_Rain_2017.csv` dataset first.  

{% capture text %}
- Select the `Open` button in the top right hand corner of OpenRefine to open a new instance of the software in your browser.  
- Create a new project using  `BOM_GCS_Rain_2017.csv`  dataset
- Name it  `BOM_GCS_Rain_2017`
- Look at both datasets, what variables do they have in common?
  - `Date`  column in  `QldShark_2017_Clean_v2`
  - `Year` ,  `Month` and  `Day` columns in  `BOM_GCS_Rain_2017`.
 
These could be used as a key to match on.  A key is a unique, matching value in one column from the dataset you are taking values from.  

At present the date is represented in three columns, `Year`, `Month` and `Day` and need to be joined up to match the `Date` column in `QldShark_2017_Clean_v2`.

We need to combine the contents of the columns, and add a specific string to the new column’s values, such as a common separator.

- Go to BOM_GCS_Rain_2017 OpenRefine project
- At  `Year`  column select  `> Edit column > join columns`
- Tick  `Year` ,  `Month`  and  `Day`  boxes
- add the separator  `-` (dash) between the content of each column so it will match the date format in `QldShark_2017_Clean_v2`
- at  `Write result in new column named`  add  `Date`
- OK.

The image below illustrates this step.{% endcapture %}{% include card.md header="Add a new column with values from three columns " text=text %}
{% include figure.html img="OpenRefineJoinColumns.png" alt="Add a column with values from three columns" caption="Joining up columns" width="100%" %}

{% include button.md text="watch this video to work through the activity" link="https://vimeo.com/422323847/ae8b0c4414" color="info" %}
