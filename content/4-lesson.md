---
title: Key
nav: true
---

# Create the new variable

Now we can extend the dataset `QldShark_2017_Clean_v1`  with a new variable  `Camera_Street_Suburb`  from the `QPSTrafficCamerasClean`  dataset. We will do this using a GREL expression `cell.cross`. The  `cell.cross`  function performs a cross or lookup between two columns in two datasets or the same dataset. It returns an array (list) of zero or more rows in the project i.e. matching against  `QPSTrafficCamerasClean`  for which the cells in their column i.e.  `Camera_Street_Suburb`  have the same content as cell  `Crash_Street_Suburb` . 

{% capture text %}
- Go to  `QLDTrafficAccident_2018`  project
- On  `Crash_Street_Suburb`  `> Edit Column> Add column based on this column>`
- name the new Column  `Camera_Street`
- enter this GREL expression:

     `cell.cross("QPSTrafficCamerasClean","Camera_Street_Suburb")[0].cells["Camera_Street"].value`
  
  - `("QPSTrafficCamerasClean","Camera_Street_Suburb")`  is the data we are looking up and matching. 
  - `[0]`  counts from the first value. 
  - `.cells[“Camera_Street”].value`  is a command to add the value from the Camera Street variable to the new column, if there is a match.

- 251 rows of traffic accident observations now have a new variable & value added of a camera located in the same street.
- `Sort`  the new column  `Camera_Street`  to view the records that have data for this new variable.

**Extra**

Let's now change the results of the cell.cross results from the name of the Camera_Street value to a boolean value of "Yes".
- Select the new column, in this case, `Camera_Street` and `Edit Cells > Transform >`
- GREL Expression:

    `if(value.contains(/./),"yes",value)`
  - This means if the value contains `(/./)` (any character found in the cell), replace it with `Yes` value.
- `Sort` `Camera_Street` again to view changes to the records.
- Close both projects.

We could have added the data from the  `Camera_Street_Suburb` column using the same steps above.{% endcapture %}{% include card.md header="Match a key variable from two datasets & add a variable using GREL cell.cross" text=text %}

The image below shows the GREL cell.cross expression in action. 
 
{% include figure.html img="ORCellCross.JPG" alt="Add a column matching with a key id using GREL cell.cross" caption="Add a column matching with a key id using GREL cell.cross" width="100%" %}

Find more information on the  `cell.cross`  function [here](https://github.com/OpenRefine/OpenRefine/wiki/GREL-Other-Functions#crosscell-c-string-projectname-string-columnname) and more GREL functions [here](https://github.com/OpenRefine/OpenRefine/wiki/GREL-Functions).


{% include button.md text="Watch the GREL cell.cross activity on this video" link="https://vimeo.com/422324961/6cc1733109" color="info" %}

----

<p align="center">
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle/content/3-lesson.html"><-- BACK</a> |
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle/content/5-lesson.html">NEXT --></a>
</p>
