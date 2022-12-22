---
title: Tidy
nav: true
---

# Tidy data - a revisit 

-----

It would be useful to add the `Distribution` variable from `NESP_SharkSpeciesList` to `QldShark_2017_Clean_v2`, but the data in that column is very messy with multiple values inside the cells. Do a `Text facet` on the `Distribution column` and explore.

To create a [tidy](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html) dataset, where:
- Each variable forms a column
- Each observation forms a row
- Each cell has one value
- Each type of observational unit forms a table,

multi-value cells need to be split by the value.

This task is helpful where there are multiple values in a cell that are not organised consistently, such as when survey respondents can select multiple, controlled values to answer a question, or a notes field has free text.  The `Distribution`  column is an example of this. Let's add the column to `QldShark_2017_Clean_v2` then tidy it.

{% capture text %}
- Go to `QldShark_2017_Clean_v2`
- Select `Common name`  column `Edit Column > Add column based on this column`
- name the new Column `Distribution`
- enter this GREL expression:

  `cell.cross("NESP_SharkSpeciesList","Common name")[0].cells["Distribution"].value`

382 rows of the shark captures now have a new variable & value of `Distribution` added.{% endcapture %}{% include card.md header="Add a new column" text=text %}

Now we need to tidy the new variable in `QldShark_2017_Clean_v2`, then split the column into two columns with a value in each.

{% capture text %}
- Go to `QldShark_2017_Clean_v2`
- Select column  `Distribution > Facet > Text Facet`
- There are 6 choices. Two of the choices contain two values within the cells e.g. Australasia & Indonesia. The multiple values do not contain a common separator.  This will need fixing to be able to split on.

Let's change the blank choice to "NULL" as these records do not have any data.
- In `Distribution` Facet box hover over `(blank)`
- Select `edit` and type `NULL` > `Apply`
- At `Distribution column` 
- Select `Edit cells > Replace > Find: & Replace with: ;`
- Select `Edit column > Split in several columns > by separator *;* > Split into *2* columns`
- `ok`.
 
 An additional Distribution column will be created with values only appearing where there had previously been two values in the original cell.{% endcapture %}{% include card.md header="Split a multi-value column" text=text %}

##### Watch these steps in this video.

<div style="padding:75% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/783496236?h=3079029ca3&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="TidySplitMultiOpenRefine.mp4"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>

Now let's explore the column `Notes on skies and wind`. It is messy and contains multiple values within the cells. Ultimately we will create multiple columns using GREL and a language known as Regular Expression or [Regex](https://en.wikipedia.org/wiki/Regular_expression), which searches for patterns in strings.  

{% capture text %}
- Go to column `Notes on skies and wind`
- Select `Facet > Text facet` and explore the 36 choices

Notice the variations in common separators, order of values and case format. We cannot split the variable into multiple columns using the method.
- Hover over the `(blank)` choice select `edit` and change `(blank)` to `NULL`
- Select `Edit cells > Common transforms > to lower case` to make the case consistent throughout the cell (and reduce the choices to 31)
- Select `Edit column> add column based on this column`
- Type new column name  `Overcast`
- Click inside expression box, enter GREL expression:
    
    `if(value.contains("overcast"),"overcast",value).replace(/.*[^overcast].*/,"")`
    
    This means...
    if (the value in the cell contains "overcast", replace it with "overcast" value), then replace (anything that is not "overcast" that is found one or more times in the cell, with "" ie. a blank).
    
- Preview and ok
- Repeat steps above for the other Sky related value `fine` (can reuse expression from  `history`  tab)

Now let's join up the two columns `fine` and `overcast` which are really values, into a new variable `Skies`
- Go to `fine` column `Edit column > Join columns...`
- Select `fine` and `overcast` from tick box list
- Select `Write result in new column named...`
- Type `Skies` and `ok`.

We now have a new variable `Skies`. Perform and text facet to see the value choices.
- Hover over `(blank)` choice select `edit` and type `NULL` and `Apply`. Now each cell has data.

Next we can extract all the "wind" data into a new variable using the steps above.

- Select `Edit column> add column based on this column`
- Type new column name  `strong breeze`
- Click inside expression box, enter GREL expression:
    
    `if(value.contains("strong breeze"),"strong breeze",value).replace(/.*[^strong breeze].*/,"")`
- Preview and ok
- Repeat steps above for the other "wind" related values that can be found in the `Text facet window` `near gale` and `light winds` (can reuse expression from  `history`  tab).

Now let's join up the 3 columns `strong breeze`, `near gale`, `light winds` which are really values, into a new variable `Wind`
- Go to `near gale` column `Edit column > Join columns...`
- Select `strong gale`, `calm winds`, `strong breeze`, `near gale`, `light winds`, `gale force`, `light breeze` from tick box list
- Select `Write result in new column named...` 
- Type `Wind` and `ok`.

We now have a new variable `Wind`. Perform a text facet to see the value choices.
- Hover over `(blank)` choice select `edit` and type `NULL` and `Apply`. Now each cell has data.
- Go to `All` column `Edit columns > Re-order / remove columns...`
- Drag and drop the following columns to remove: `fine`, `overcast`, `Notes on skies and wind` , `near gale` , `strong breeze`, `light winds`
- `ok`.

This great [GREL cheat sheet](https://code4libtoronto.github.io/2018-10-12-access/GoogleRefineCheatSheets.pdf) from [code4lib Toronto](https://code4libtoronto.github.io/) has more details on building expressions using Regex.
{% endcapture %}{% include card.md header="Add new columns using GREL & Regex" text=text %}

See how this works in the video below.


------

The final step is to export specific variables from this tidy dataset to a .csv file which can be parsed (understood by) the geo.json tool used in the next lesson.

{% capture text %}
- Go to  `All` column  `>Edit Columns> Reorder Remove columns`
- Drag and drop the columns not needed including `Species Code`, `Date`, `Area`, `Location`, ` Genus`, `Species`, `Distribution`, `Distribution1`,  to the  `remove` box.
- `Common name`, `Latitude`, `Longitude`, `Length (m)`, `Rainfall_mm`, `Formatted Date`, `Water Temp (C)`, `Skies`, `Wind`  will remain
- `Ok`
- Click `Export` button, top right hand corner
- Select Comma-separated value dataset
- save file{% endcapture %} {% include card.md header="Export selected columns to .csv file" text=text %}

----

<p align="center">
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle/content/4-lesson.html"><-- BACK</a> |
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle/content/6-lesson.html">NEXT --></a>
</p>


