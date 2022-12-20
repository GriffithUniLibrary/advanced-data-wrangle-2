---
title: Create
nav: true
---

# Create the project
----

{% capture text %}
**Windows**: double-click on the `openrefine.exe` file. Java services will start automatically on your machine, and OpenRefine will open in your browser. Be sure to use either Chrome or Firefox, as OpenRefine does not play well with Microsoft Edge or Safari.

**Mac**: OpenRefine can be launched from your Applications folder.

**Linux**: navigate to your OpenRefine directory in the command line and enter `./refine`.

Once OpenRefine is launched in your browser, the home screen displays options to `Create Project`, `Open Project`, or `Import Project`. 

Select `Create a project`.

**If launch fails**

If OpenRefine does not automatically open within your browser after launch, point your browser at `http://127.0.0.1:3333/` or `http://localhost:3333` to launch the program.{% endcapture %}
{% include card.md header="Launch OpenRefine" text=text %}


{% capture text %}
- Choose `Create Project`
- Select `Get data from this Computer`.
- Select `Choose Files` and browse to select the file `QldShark_2017_Clean_v1.csv` you saved to your `Downloads` folder.
- Either click `Open` or double-click on the filename to import it into OpenRefine.
- Click `Next`.{% endcapture %}
{% include card.md header="Upload data from your computer" text=text %}


{% capture text %}
- Choose `UTF8` as the method of encoding as this should convert any 'smart' formatting into plain text.
- Give the project a meaningful name such as `QLDShark_2017_Clean_v2`
- If all looks fine, click  `Create Project`.{% endcapture %}
{% include card.md header="Preview the data" text=text %}

The original dataset presents details of numbers of sharks caught in the Shark Control program by species, date of capture and location and other variables. This version of the dataset has ten variables.  Take a look at each variable in the columns presented.

Let's now try to add a few more variables to the dataset.

##### Watch this video from the introductory workshop for a revision on the steps to launch OpenRefine.
<div style="padding:75% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/780970002?h=79b8c70261&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="CreateProjectOR.mp4"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
