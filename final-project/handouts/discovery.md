# <i class="fas fa-book fa-fw"></i> Discovery Document

## Overview
You will deliver the following:  
* A Google Document (described below).
* A Link to a Google Folder that holds all your **raw data**. Your link will be in the document.  
* Target Challenge Goals

You do not need to have any code written yet, but you may want to use some code to help you learn about the data. For example, you may want to print out the columns or get some statistical information about the data using code.  

You can use Excel or other tools to view the data.  

Things NOT necessary for this deliverable:  
* web scraping  
* data clean up  
* unit testing  
* plots  
* report  
* presentation  

## Document Purpose 
It is a frequent student behavior to dive into a research project without fully understanding what data is available and challenges ahead. This deliverable is to assure that the student has the necessary data and has the understanding of the pending challenges.  

The Discovery Document's purpose is to:  
1) Illustrate that you have found **appropriate data**. The data must be:
    * Large enough (500 lines or more)  
    * Available for download (CSV file format)   
    * Has the necessary information to successfully conduct your research  
2) Present a few **questions** (about the data)  
    * This is the focal point of your research  
    * Express why your questions are of interest (motivation)  
3) Illustrate that you **understand the data**:  
    * Know how the data was sourced
    * Know how the data may be limited (reliability, accuracy, completeness, messy)  
    * Identify & explain relevant columns: names, format, units, ranges, cleanliness  
    * Issues or challenges in working with the data (e.g. too big, non-standard key formatting making cross-referencing difficult, missing information, too broad or narrow)  
4) Establish **Challenge Goals**:  
    * While this may change, it is important to consider what challenges you intend to take on. See below for more details.  


## Document Sections
Your document will have the following sections:  
* **Title and Author(s).** The title should reflect your specific research questions (not just “CSE 163 Project”).  
* **Summary of research questions.** Give a numbered list of 3 or more research questions and a brief description of what you will investigate. Each research question should have 1–3 sentences and propose something that can be definitively answered, not just a general topic or area of investigation.  
* **Motivation.** In one or two paragraphs, expand on your research questions by providing context about why you care, or why anyone should care. How does knowing the answers affect the world or our understanding of it?  
* **Dataset.** This is the MOST important part of this document. (more details below) You will do the following. 
    * Describe the real, existing dataset that you will use, including exact URLs.  
    * You may not use a dataset that has been used in a previous CSE 163 assignment, AP Research work, or competition (TSA, FBLA).  
    * The data must be real — neither you nor someone else may make up the data.  
    * The data must be large enough (500 lines or more).  
* **Challenge goals.** 
    * Select at least 2 challenge goals that you are planning to meet.  
    * Justify why you think this challenge goal is a good fit for your project.  

## Dataset Section
You need to list out all your datasets, sources, caveats, important columns, data values, and relevent information. This section should contain multiple tables or other easy to read formats. While you may copy some information from your datasource, it is critical that you understand the data.  

You should:  
* List all datasets  
* List important columns from each dataset  
* Examine challenges with the data  

Here is an short example. Your dataset documentation is likely to be longer!   

```{admonition} Sample Writeup
:class: note
**Datasets Summary:**   
All the data can be found on this [Google Folder](https://support.google.com/drive/answer/7166529?hl=en).  

This shows that we are using only three datasets.     

|DataSet|Source|Size|Notes|
|-------|------|----|-----|
|graduation_2018.csv|<span title="Your link must be a deep link that goes to the data!" style="background-color: yellow"><a href="https://data.gov">data.gov</a></span>|800x40|Contains high school graduation rates by Washington State school district in 2018. Data was collected by the districts self-reporting.|
|teachers_2014.csv|<a href="https://data.gov">data.gov</a>|48x10|Contains full-time teacher pay and benefits by school district|
|geo_wa_counties.json|[Natural Earth](https://www.naturalearthdata.com/downloads/50m-cultural-vectors/)|NA|Contains geometry data for the counties in Washington state|

**Graduation_2018.csv**  
This dataset contains graduation rates of high school students in the year 2018 only. The rates are by race and school district.  
|Column|Description|
|------|-----------|
|district|string: The name of the school district|
|county|[string]: A list of county names that the school district is in. A district may span multiple counties|
|race|string: The race of the students in this row. Races included are ['white', 'hispanic', 'black', 'asian', 'multi']|
|4YGR|double: The percent of students of this race that graduated high school in four years. If a student graduated in 5 years, another column tracks that.|

**Teachers_2014.csv**  
This dataset contains salary & benefits information for full-time teachers by school district in the year 2014.  
|Column|Description|
|------|-----------|
|DNUM|integer: The number for the school district. For example, Northshore is 417.|
|PERV|integer: The number of personal vacation days that a teacher gets per year.|
|BASE|double: The Base salary of a full-time teacher.|
|HRPAY|double: The additional pay given to a teacher beyond their base salary for simply being a teacher.|
|SPST|double: The average additional pay (stipend) given to a teacher for coaching a sport.|
|APST|double: The additional pay (stipend) given to an AP Teacher.|

**Data Challenges**  
The datasets come from different years because we could not get accurate data for both sets during the same year. If we correlate the data across different years, we are not representing the true data. We need to highlight this!  

While the teacher pay dataset is extensive, there is no single column that gives a simple summary how much an "average" teacher makes. This is because we don't know how many teachers receive certain types of stipends.   

It would be valuable to track the changes of graduation rates over time as related to the changes of salary over time. I will be doing some extra work to find more datasets to allow graphing over time.  

The School Districts don't map easily across datasets. One dataset uses a number while the other uses a string. I may need to manually create a mapping dataset that allows me to join the two together.  

It would be good to geospatially plot graduation rates, but the geometry data that I've found so far is only by county while the school districts can span many counties. I may have to manually pick, or randomly guess, which county a school district mostly represents. Or, perhaps I can locate geometry for the school districts themselves. 
```
## Challenges
Challenge goals help us to define expectations while still offering flexibility for you to design your own project. Meeting the requirements of a challenge goal is described here. 

* **Valuable Unit Testing**: To qualify, you must deliver valuable Unit Tests of the methods that clean and organize your data. You need to provide some fake data and run the tests that validate the results. You should consider using Python's Unit Test framework. Look at past Checkpoints in `Replit` where there was a `run_tests.py` file. Copy that infrastructure.  
* **Multiple Datasets**: To qualify, you must work with **four** or more datasets what require **merging** together in various ways. The merging must be necessary to come up with a richer analysis. This requirement is not just about using more than one dataset across your research questions, but is more about combining (via **merge**) the datasets to make a more in-depth analysis.  
* **Web Scraping or API Usage**: To qualify, you must successfully scrape hundreds of rows of data off one or more web page. Or, you must use some public API to collect data from some data service (e.g. Spotify). The resulting data would be saved as a CSV file for later organization and analysis. To Web Scrape, consider using [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/).  
* **Statistical Validation**: To qualify, you must do some extra work on top of your results to verify the validity of the results. For example, using some test of statistical significance to verify your results aren’t likely to happen by chance. The statistical analysis needs to be visible in the plots themselves and briefly discussed in your write-ups. You cannot simply use `seaborn` to plot a regression and consider this challenge fulfilled.   
* **Machine Learning**: Many students have attempted this with great failure. This challenge goal requires going above and beyond the fundamental steps of a Machine Learning pipeline we introduced in class. You cannot simply create a model, present some accuracy number and call it quits. To qualify you need to:
    * Explore and use a new Machine Learning model: You cannot use the simple `DecisionTree`. Work to adjust the hyperparameters during training to improve the model's accuracy. You must then **PRESENT** your exploration during the Final Presentation.  
    * Explore the predictions made by the model to either:   
        a) provide insight into how the model makes its predictions. You can look at <a href="../../Topics/machine_learning/regression.html"> Machine Learning -> Regression-Distance Study</a> Look at how the Model Graphs provide clear insight into how the model makes predictions.  
        b) make some predictions about the future or situation not present in the data.  
    * Dive deep into applying machine learning to your dataset to gain insights about the data or use it to make predictions about the future. Be explicit with what your goal is and how you will assess if you meet that goal. One example could be looking at various model types (and different settings of their hyperparameters) to identify which model is “best” (by how you define best). Another could be looking at how to use an “interpretable model” to understand which features are the most informative for how a decision is made. This challenge goal requires going above and beyond the fundamental steps of a Machine Learning pipeline we introduced in class. To achieve this challenge goal, you need to demonstrate exploration of more ideas in machine learning. 
* **New Library**: Learn a new Python library and use it in your project in a significant way to help with your analysis. Part of this class is being able to learn libraries in Python. Show that you are able to take what you’ve learned in the context of learning a library we have not discussed in-depth in this course. Here are some recommended libraries.
    * Download from Web: [requests](https://2.python-requests.org/en/master/)
    * Scientific Computing: [SciPy](https://www.scipy.org/)
    * Natural Language Processing: [spaCy](https://spacy.io/)
    * Advanced/Interactive Visualizations: [altair](https://altair-viz.github.io/) or [plotly](https://plot.ly/python/).  
        * Note that interactive plots work best for data that has lots of different filtering options. For example: filter by year, by age, by gender, by position. 
    
```{admonition} Interactive Note
:class: important
Note that you need to **make a video** of the interaction with your plots.  
```

## Sources of Data
The best approach is to start with a problem that interests you, and then look for data. However, if you are creative and critical, you can go the other way around: start with the data and then identify areas of research.    

There are MANY sources of data and you can seek out anything and everything you can get your hands on. Google will be your friend for finding a dataset.Here are some sources for you to explore:  

* A variety of data sets are available from [UW Libraries](http://guides.lib.washington.edu/content.php?pid=135867&sid=1165959)  

* [Awesome Public Datasets](https://github.com/awesomedata/awesome-public-datasets) - large variety of maintained data sets  

* [Baron Schwartz’s list of datasets](http://www.mysqlperformanceblog.com/2011/02/01/sample-datasets-for-benchmarking-and-testing/). Some of these are themselves rich lists of datasets, such as the Amazon AWS public data sets.  

* [Data.gov](http://www.data.gov/) for U.S. open government data, [data.wa.gov](https://data.wa.gov/) for Washington state open government data, and [data.seattle.gov](https://data.seattle.gov/) for Seattle open government data  

* [SQLShare](https://sqlshare.escience.washington.edu/): public scientific datasets. Some require considerable knowledge to interpret, others are easier to understand. You can select “All datasets” and then filter by keyword, or you can select a tag from among those in the left column.  

* [Reddit Data Sets](https://www.reddit.com/r/datasets/)  

* [Civic Data Sets for the Pacific Northwest](http://nwdata.org/)  

* [An archive of datasets distributed with the R statistical language](https://vincentarelbundock.github.io/Rdatasets/)

* [30 Places to Find Open Data on the Web Visual.ly](http://blog.visual.ly/data-sources/)  

* [Office for National Statistics (UK)](http://www.statistics.gov.uk/default.asp) a repository of detailed statistics about Great Britain and Northern Ireland  

* [World Bank Data Catalog](http://data.worldbank.org/data-catalog)  

* [CDC NCHS Data](http://www.cdc.gov/nchs/data_access/data_tools.htm) - CDC’s National Center for Health Statistics Data Access  

* [Machine Learning Repository](http://archive.ics.uci.edu/ml/) - large variety of maintained data sets  

* [For datasets used in CSE 163 Lessons](https://courses.cs.washington.edu/courses/cse163/21su/files/data/lecture-readings) (remember, these can’t be the central part of your project)

