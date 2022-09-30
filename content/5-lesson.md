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

Now we need to tidy the new variable in `QldShark_2017_Clean_v2`. The following method uses GREL and a language known as Regular Expression or [Regex](https://en.wikipedia.org/wiki/Regular_expression), which searches for patterns in strings. 

{% capture text %}
- Go to`QldShark_2017_Clean_v2`
- Select column  `Distribution` > Facet > Text Facet`
- There are 5 choices, a few less than in the "NESP_SharkSpeciesList" so less tidying.  Make a note of the distribution names including, `Australasia`, `Cosmopolitan`, `Indo-Pacific`, `Indo-West Pacific`, Indo-West Pacific`, ` 

- Select column  `Distribution` > Edit column> add column based on this column`

- Type new column name  `Universal access toilet`
- Click inside expression box, enter GREL expression:
    
    `if(value.contains("Universal access toilet"),"Yes",value).replace(/.*[^Yes].*/,"")`
    
    This means...
    if (the value in the cell contains "Universal access toilet", replace it with "Yes" value), then replace (anything that is not "Yes" that is found one or more times in the cell, with "" ie. a blank).
    
- Preview and ok
- Repeat steps above for each of the items owned (can reuse expression from  `history`  tab)

This great [GREL cheat sheet](https://code4libtoronto.github.io/2018-10-12-access/GoogleRefineCheatSheets.pdf) from [code4lib Toronto](https://code4libtoronto.github.io/) has more details on building expressions using Regex.
{% endcapture %}{% include card.md header="Add a new column using GREL & Regex" text=text %}

See how this works below.

{% include figure.html img="ORRegex.JPG" alt="Using Regex" caption="Using Regex" width="100%" %}

{% include button.md text="Watch the steps above on this video" link="https://vimeo.com/422342110/15f6fa71c1" color="info" %}

------

Let's now change the blank cells to a  `“No”`  value.
{% capture text %}
- Go to each new column and  `Facet > Text Facet`
- Hover over  `(blank)` and select edit 
- Change  `(blank)` to  `No` , ` apply` and close facet
- Repeat on each column{% endcapture %} {% include card.md header="Fill all blank cells in new columns with a value" text=text %}
Each location now has a column for the variables,  `table`,  `play area`,  `universal access toilet`  and  `water`,  with a  `yes` or  `no`  value.

The final step is to export specific variables from this tidy dataset to a .csv file which can be parsed (understood by) the geo.json tool used in the next lesson.

{% capture text %}
- Go to  `All` column  `>Edit Columns> Reorder Remove columns`
- Drag and drop the columns not needed including `Site Features`, `Site specific alerts`, `Site and Access Comments`, `GPS coordinates`, `Access Direction`, `Upcoming operation dates`, `signed`, `camping limitations` to the `remove` box.
- `Title`, `Latitude`, `Longitude`, `Location Description`, `Water`, `Universal access toilet`, `Table`, `Play area`, `Barbecue`  will remain
- Ok
- Click `Export` button, top right hand corner
- Select Comma-separated value dataset
- save file{% endcapture %} {% include card.md header="Export selected columns to .csv file" text=text %}

{% capture text %}
Joining up columns is straightforward if the values within the rows are unique.  

In this instance the values were not unique,  all were `Yes` or `No`.  

Someone asked about this in a class, so I experimented.  
 
This is the process and expression that was most successful.
- Select the column, in this case, `Play area` and `Edit Column > Add a column based on this column >`
- Name column `Site Features`
- GREL Expression:

  `value.replace("Yes","Play area").replace("No","") + " ; " + cells["Table"].value.replace("Yes","Table").replace("No","") + " ; " + cells["Water"].value.replace("Yes","Water").replace("No","") + " ; " + cells["Universal access toilet"].value.replace("Yes","Universal access toilet").replace("No","")`
 
This replaces the `Yes` values with a `named value` relevant to the column it is within and replaces a `No` value with nothing.  
 
It adds values from additional columns with the `+ cells` and does the same value replace with each.  
 
It also places a separator between each result.  This results in a number of extra `;` separators however, due to some empty `""` values.  These can be removed in the new column with:
 
- Select `Site Features` column
- `Edit cells > Transform`
- GREL Expression:
   `value.replace(/^\W*/,"").replace(/\W*$/,"").trim()`
   
This Regrex expression inside `//` means remove from the front of a cell `^`  any non word `\W` found 0 or more times `*` and replace it with nothing `,""` , then remove from the end of a cell `$` any non word `\W` found 0 or more times `*` and replace with nothing `,''`.  

The final `.trim` removes any remaining leading or trailing whitespace.

{% endcapture %} {% include card.md header="But wait....there's more...

reverse engineer the Site Features wrangling work" text=text %}
----

<p align="center">
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle/content/4-lesson.html"><-- BACK</a> |
  <a href="https://griffithunilibrary.github.io/advanced-data-wrangle/content/6-lesson.html">NEXT --></a>
</p>


