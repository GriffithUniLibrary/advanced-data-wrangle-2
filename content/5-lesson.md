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

Now we need to tidy the new variable in `QldShark_2017_Clean_v2`, The then split the column into two columns with a value in each.

{% capture text %}
- Go to `QldShark_2017_Clean_v2`
- Select column  `Distribution > Facet > Text Facet`
- There are 7 choices. Two of the choice show two values within e.g. Australasia & Indonesia. The multiple do not contain a common separator, which will need fixing to be able to split on.

Let's change the blank choice to "NULL" as these records do not have any data.
- In `Distribution` Facet box hover over `(blank)`
- Select `edit` and type `NULL` > `Apply`
- At `Distribution column` 
- Select `Edit cells > Replace > Find: & Replace with: ;`
- Select `Edit column > Split in several columns > by separator *;* > Split into *2* columns`
- `ok`.
 
 An additional Distribution column will be created with values only appearing where there had previously been two values in the original cell.  
{% endcapture %}{% include card.md header="Split a multi-value column" text=text %}

Now let's explore the column `Notes on skies and wind`. It is messy and contains multiple values within the cells. Ultimately we will create multiple columns using GREL and a language known as Regular Expression or [Regex](https://en.wikipedia.org/wiki/Regular_expression), which searches for patterns in strings.  

{% capture text %}
- 
- Repeat steps above for each of the Distribution location names, making new column names Distribution2, Distribution3 etc. (can reuse expression from  `history`  tab)
- Go to column  `Site features` > `Edit column> add column based on this column`
- Type new column name  `Universal access toilet`
- Click inside expression box, enter GREL expression:
    
    `if(value.contains("Universal access toilet"),"Yes",value).replace(/.*[^Yes].*/,"")`
    
    This means...
    if (the value in the cell contains "Universal access toilet", replace it with "Yes" value), then replace (anything that is not "Yes" that is found one or more times in the cell, with "" ie. a blank).
    
- Preview and ok
- Repeat steps above for each of the items owned (can reuse expression from  `history`  tab)
- Repeat steps above for each of the Distribution location names, making new column names Distribution2, Distribution3 etc. (can reuse expression from  `history`  tab)
This great [GREL cheat sheet](https://code4libtoronto.github.io/2018-10-12-access/GoogleRefineCheatSheets.pdf) from [code4lib Toronto](https://code4libtoronto.github.io/) has more details on building expressions using Regex.
{% endcapture %}{% include card.md header="Add a new column using GREL & Regex" text=text %}

See how this works below.

{% include figure.html img="ORRegex.JPG" alt="Using Regex" caption="Using Regex" width="100%" %}

{% include button.md text="Watch the steps above on this video - Soon" link="" color="info" %}

------

The final step is to export specific variables from this tidy dataset to a .csv file which can be parsed (understood by) the geo.json tool used in the next lesson.

{% capture text %}
- Go to  `All` column  `>Edit Columns> Reorder Remove columns`
- Drag and drop the columns not needed including `Site Features`, `Site specific alerts`, `Site and Access Comments`, `GPS coordinates`, `Access Direction`, `Upcoming operation dates`, `signed`, `camping limitations` to the `remove` box.
- `Title`, `Latitude`, `Longitude`, `Location Description`, `Water`, `Universal access toilet`, `Table`, `Play area`, `Barbecue`  will remain
- Ok
- Click `Export` button, top right hand corner
- Select Comma-separated value dataset
- save file{% endcapture %} {% include card.md header="Export selected columns to .csv file" text=text %}

----

<p align="center">
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle/content/4-lesson.html"><-- BACK</a> |
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle/content/6-lesson.html">NEXT --></a>
</p>


