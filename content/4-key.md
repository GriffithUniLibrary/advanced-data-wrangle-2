---
title: Key
nav: true
---

# Create new variables

Now we can extend the dataset `QldShark_2017_Clean_v2`  with a new variable  `Rainfall_mm`  from the `BOM_GCS_Rain_2017`  dataset. We will do this using a GREL expression `cell.cross`. 

The  `cell.cross`  function performs a cross or lookup between two columns in two datasets or the same dataset. It returns an array (list) of zero or more rows in the project i.e. matching against  `BOM_GCS_Rain_2017`  for which the cells in the column i.e.  `Date`  have the same content as cell  `Date` . 

{% capture text %}
- Go to  `QldShark_2017_Clean_v2`  project
Firstly let's transform the `Date` column to a date format.
- Select `Date` column > Edit cells > Common transforms > To date`

Now
- Select `Area` column `> Facet > Text Facet`
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
- `x` close the Text Facet window.{% endcapture %}{% include card.md header="Match a key variable and add a new variable using GREL cell.cross" text=text %}


The image below shows the GREL cell.cross expression in action. 
 
{% include figure.html img="OpenRefineCellCrossShark.PNG" alt="Add a column matching with a key id using GREL cell.cross" caption="Add a column matching with a key id using GREL cell.cross" width="100%" %}

##### Follow the steps in this video.

<div style="padding:75% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/783103369?h=926498486d&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="GRELCellCross.mp4"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>


Let's now extend the dataset `QldShark_2017_Clean_v2`  with another variable  `Species`  from the `NESP_SharkSpeciesList.csv`  dataset. 


{% capture text %}
`QldShark_2017_Clean_v2` currently contains a variable `Species Name` , but the values are actually common names the sharks are known by. Let's change the variable name.
- Go to  `QldShark_2017_Clean_v2`  project
- Select `Species Name` column `> Edit column > Rename this column`
- name it `Common name` 
- `Ok`.

Next: 

- Select the Open button in the top right hand corner of OpenRefine to open a new instance of the software in your browser.
- Create a new project using `NESP_SharkSpeciesList.csv` file
- Name it `NESP_SharkSpeciesList`
- Look at both datasets, what variables do they have in common?
  - `Common name` in ``NESP_SharkSpeciesList.csv`
  - `Common name` in `NESP_SharkSpeciesList`.
 - Go to `Common name` for each dataset
 - `Facet > Text facet`

Take a look at the names in each. The `NESP_SharkSpeciesList` dataset contains an authoritative list of Shark common names, Species, Genus, Family and Order names from a scientific project. The `QldShark_2017_Clean_v2` list of names is not authoritative, and many of the shark common names are variations or incorrect.  We need to correct the following:

All the "Whaler" names in `QldShark_2017_Clean_v2` need to be changed to "Shark" as the only Whalers identified in `NESP_SharkSpeciesList` were Bronze and Creek Whaler.  You can perform a filter on `whaler` to check.

We need to clean the inconsistent names to then match the values in the key variable accurately.
- Go to `Common name` in `QldShark_2017_Clean_v2`
- `Edit cells > Replace`
- Find: `whaler`
- tick `case insensitive`
- Replace with: `Shark`
- `Ok`.

Then on the same column:
- `Facet > Text Facet`

The first shark name is an abbreviation let's make it a full name.
- highlight `Aus Sharpnose Shark` > `Edit` 
- Change to `Australian Sharpnose Shark` > `Apply`
- Leave the `Text facet` window open.

We want to match on unique values in the variables, and at present many of the shark names in `QldShark_2017_Clean_v2` are missing the term "Shark" in their title.  We can check them against the Common name's in `NESP_SharkSpeciesList`.

- Look through the `Text Facet` list in `QldShark_2017_Clean_v2` for names without `Shark` in their name.  These include:
 - `Australian Blacktip`, `Great Hammerhead`, `Mako` and `Wobbegong`

- Go to `Common name` in `NESP_SharkSpeciesList` > `Text filter`
- type `Australian Blacktip`
  - note the results that the common name needs `Shark` added. Make this change in `QldShark_2017_Clean_v2`
- now type `Great Hammerhead` in the `Text filter`
  - note the results are the same, so no changes needed
- perform a filter for each of the four names above and check if correctly named.
 - note that `Mako` and `Wobegong` are generic names and we can't identify the species exactly, so we won't be able to match on these.

Now that we have cleaned up as many inconsistancies possible, let's match the key variables: 
- Go to `QldShark_2017_Clean_v2` project
- at `Common name` select `Edit Column > Add column based on this column`
- name the new Column  `Species`
- enter this GREL expression: *(tip: you can reuse and make changes to previous expressions using the `History` tab)*

     `cell.cross("NESP_SharkSpeciesList","Common name")[0].cells["Species"].value`
     
- Preview and `ok`.

382 rows of the shark captures now have a new variable & value of `Species` added.
- `x` close the Text Facet window.

*Challenge*: Try adding the `Genus` variable using the same steps as above.{% endcapture %}{% include card.md header="Tidy the data then match a key variable using GREL cell.cross" text=text %}

Find more information on the  `cell.cross`  function [here](https://docs.openrefine.org/manual/grelfunctions#other-functions) and more GREL functions [here](https://docs.openrefine.org/manual/grelfunctions).

##### Watch the GREL cell.cross activity on this video

<div style="padding:66.59% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/783187069?h=17c66541b0&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="Tidy data then match a key variable using GREL cell.cross"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>

----

<p align="center">
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle-2/content/3-find.html"><-- BACK</a> |
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle-2/content/content/5-tidy.html">NEXT --></a>
</p>
