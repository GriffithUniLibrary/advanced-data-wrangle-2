---
title: Key
nav: true
---

# Create the new variable

Now we can extend the dataset `QldShark_2017_Clean_v2`  with a new variable  `Rainfall_mm`  from the `BOM_GCS_Rain_2017`  dataset. We will do this using a GREL expression `cell.cross`. The  `cell.cross`  function performs a cross or lookup between two columns in two datasets or the same dataset. It returns an array (list) of zero or more rows in the project i.e. matching against  `BOM_GCS_Rain_2017`  for which the cells in the column i.e.  `Date`  have the same content as cell  `Date` . 

{% capture text %}
- Go to  `QldShark_2017_Clean_v2`  project
- Select `Area` column ` > Facet > Text Facet`
- Select `Gold Coast` from Text Facet results menu

 56 resulting matching rows will display which you can now work with. 
 
- On  `Date` select `Edit Column > Add column based on this column`
- name the new Column  `Rainfall_mm`
- enter this GREL expression:

     `cell.cross("BOM_GCS_Rain_2017","Date")[0].cells["Rainfall_mm"].value`
  
  - `("BOM_GCS_Rain_2017","Date")`  is the data we are looking up and matching. 
  - `[0]`  counts from the first value. 
  - `.cells[“Rainfall_mm”].value`  is a command to add the value from the Rainfall_mm variable to the new column, if there is a match.

- 56 rows of the shark captures now have a new variable & value of rainfall added.
- `x` close the Text Facet window.


The image below shows the GREL cell.cross expression in action. 
 
{% include figure.html img="OpenRefineCellCrossShark.PNG" alt="Add a column matching with a key id using GREL cell.cross" caption="Add a column matching with a key id using GREL cell.cross" width="100%" %}

Find more information on the  `cell.cross`  function [here](https://docs.openrefine.org/manual/grelfunctions#other-functions) and more GREL functions [here](https://docs.openrefine.org/manual/grelfunctions).


{% include button.md text="Watch the GREL cell.cross activity on this video - soon" link="" color="info" %}

----

<p align="center">
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle/content/3-lesson.html"><-- BACK</a> |
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle/content/5-lesson.html">NEXT --></a>
</p>
