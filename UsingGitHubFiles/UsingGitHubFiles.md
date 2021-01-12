---
title: "Using GitHub Files Directly from GitHub"
author: "Skyler Elmstrom"
date: "1/12/2021"
output:
  html_document:
    code_folding: show
    code_download: true
    keep_md: true
---



## **Loading Data Files From Other Repositories**
<br>
Files within a GitHub repository can be accessed directly! This includes tabular data, images, other R files, etc. Here is how:

1. Get the `raw` web address of the file you need access to via GitHub
    + Go to file in GitHub
    + Right-click the `Raw` button, click `Copy link address` for `Raw` file address
2. Load the data by pointing to that web address instead of a local file

For example, say we wanted to use a portion of Eric's Benthic WQ data and analysis:
<br><br>

-----

### Loading Eric's Data


```r
library(tidyverse)

# Eric's Benthic WQ data - https://github.com/WWU-IETC-R-Collab/MI-Analysis/main/data/ceden_benthic_WQ.csv

com.dates <- read.csv("https://raw.githubusercontent.com/WWU-IETC-R-Collab/MI-Analysis/main/data/ceden_benthic_WQ.csv")

knitr::kable(com.dates[1:5,1:5]) # first 5 rows and columns of Eric's data to show it works
```



|  X|StationCode |SampleDate |Subregion.x      |StationName.x                       |
|--:|:-----------|:----------|:----------------|:-----------------------------------|
|  1|510STODWx   |2014-06-18 |Sacramento River |Stone Lakes                         |
|  2|543R00137   |2012-05-15 |Confluence       |Deer Cr_137-543R00137               |
|  3|543R01103   |2015-04-21 |Confluence       |West Antioch Creek                  |
|  4|544CCC001   |2011-06-06 |Confluence       |San Joaquin in Antioch Ship Channel |
|  5|544CCC001   |2011-07-06 |Confluence       |San Joaquin in Antioch Ship Channel |

We can now run our modifications to this data for our own purposes without editing the original.
<br><br>

-----

### Loading an Image from a Different Repository

<br>

Then, say we wanted to include a chart created from another repository. We'd do this a little differently.

1. Get regular address of image on GitHub
2. Add `raw/` before the `branch` i.e. `main` and remove `blob` between the repository name and branch name

Here is what the R markdown syntax and new address will look like:
```
![](https://github.com/WWU-IETC-R-Collab/ClipToProjectBoundary/raw/main/SFEI_JoinLocationToParticles_files/figure-html/Subset-sf-1.png)
```

And here is the image we grabbed:
<br>

![](https://github.com/WWU-IETC-R-Collab/ClipToProjectBoundary/raw/main/SFEI_JoinLocationToParticles_files/figure-html/Subset-sf-1.png)

This method is most useful if you do not plan on making changes to the original data or files (which we should NOT be doing). Loading data this way will create a temporary, local copy in your R session that is not saved to your own repository.

There are some clever R coders who have figured out how to automate the conversion of [GitHub addresses](https://stackoverflow.com/questions/11237715/how-to-display-images-in-markdown-on-github-generated-from-knitr-without-using-e).
<br>

-----

### Pitfalls of Note

<br>
There are a few key things to keep in mind when accessing files this way:

1. If the name of the original file changes, the link in your own document to that file will break and no longer work
2. This does not create a copy of the data as a data file
3. This does not allow you to edit/change the original file

Make sure that if you use these methods that the underlying data is permanent. Otherwise, we may need to update the links when a file is deleted or renamed.
<br><br>

