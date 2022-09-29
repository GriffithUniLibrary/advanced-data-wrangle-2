---
title: Tidy
nav: true
---

# Tidy data - a revisit 

-----

It would be useful to add the `Distribution` variable from NESP_SharkSpeciesList to QldShark_2017_Clean_v2, but there are multiple values inside the celss of `Distribution`.

To create a [tidy](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html) dataset, where:
- Each variable forms a column
- Each observation forms a row
- Each cell has one value
- Each type of observational unit forms a table.

multi-value cells need to be split by the value.

This task is helpful where there are multiple values in a cell that are not organised consistently, such as when survey respondents can select multiple, controlled values to answer a question.  The `Distribution`  column is an example of this. 

{% capture text %}
- Go to  `Distribution`  column `Facet > Text Facet >` to see multiple values in a messy state.

There are a couple of ways to create new columns and move the values to these. The first method requires some cleaning of the data, followed by a GREL command `value.split` with a common separator. 

We want to perform a facet by splitting the value, using a common separator.  `Distribution` values do not have common separators, they include `&` `; ` and there appears to be some inconsistencies in the names, with 19 name choices.  Let's sort out the inconsistencies first by trying `leading and trailing whitespace` removal.
- `Edit cells > Common transforms > Trim leading and trailing whitespace'
- this fixes 3 values and reduces the Facet to 18 name choices.

Now lets' change the random separators to one common separator. 

- `Edit Cells > Transform`  and 
- GREL expression:  value.replace("&",";")
- 'Ok'.{% endcapture %} {% include card.md header="Tidy the 'Distribution' column" text=text %}

{% include button.md text="Watch the steps above on this video- soon" link="" color="info" %}

-----

The next step is to split the values so they can be moved to separate columns. 

{% capture text %}
- `Edit cells > Split multi-value cells > by Separator add: ; `
- `Edit cells > Common transforms > Trim leading and trailing whitespace'` 
- Click on first Facet result  `Play area` , with 11 results
- Go to column  `Site features > Edit column> add column based on this column`
- This removes whitespace around 40 values.
- Click inside expression box, delete  `value`  and type `"Yes"`
- `Facet > Text facet` to view the Distribution choice
- Repeat steps above for each of the items owned (can reuse GREL expression from  `history`  tab){% endcapture %} {% include card.md header="Add a new column using value.split" text=text %}

The image below shows the creation of the  `Play area`  column using the method described above.

{% include figure.html img="ORFacetSplit.JPG" alt="Custom Facet plus add a column" caption="Facet by GREL value.split & Add a column" width="100%" %}

{% include button.md text="See how to perform the value.split function on this video" link="https://vimeo.com/423061477/90ba3be431 " color="info" %}
 
-----

Below is an alternative method using GREL and a language known as Regular Expression or [Regex](https://en.wikipedia.org/wiki/Regular_expression), which searches for patterns in strings.  

{% capture text %}
- `Undo`  your steps back to Step `0. Create Project` to try this method.- 
- Go to column  `Site features` > `Edit column> add column based on this column`
- Type new column name  `Universal access toilet`
- Click inside expression box, enter GREL expression:
    
    `if(value.contains("Universal access toilet"),"Yes",value).replace(/.*[^Yes].*/,"")`
    
    This means...
    if (the value in the cell contains "Universal access toilet", replace it with "Yes" value), then replace (anything that is not "Yes" that is found one or more times in the cell, with "" ie. a blank).
    
- Preview and ok
- Repeat steps above for each of the items owned (can reuse expression from  `history`  tab)

This great [GREL cheat sheet](https://code4libtoronto.github.io/2018-10-12-access/GoogleRefineCheatSheets.pdf) from [code4lib Toronto](https://code4libtoronto.github.io/) has more details on building expressions using Regex.
{% endcapture %} {% include card.md header="Alternative method - add a new column using GREL & Regex" text=text %}

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


