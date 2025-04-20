# <i class="fas fa-book fa-fw"></i> Discovery Tips

## Overview
The point of this Deliverable is to assure that you understand your goals, your data, and that your data is sufficient.  

There are several things you must provide:  
* Downloaded & Accessible Data  
* Research Questions & Motivation  
* Data Description  
* Challenge Description  

## Downloaded Data
The data you download can come in many forms. Ultimately, you want to land on a format that your code can work with, CSV. This may mean that you originally download an Excel file and then save it as CSV. If you do any manual alterations, state the steps you took in this document.

It is better to have more data than not enough. If your data is especially large, you will work to reduce it to a more manageable size in the second deliverable (Organize). 

## Research Questions & Motivation
A common mistake in a research project is to not have a research goal in mind. Students can seek out data and then aimlessly proceed to execute an exploratory process without direction. While exploration is certainly part of Data Science, you should have some specific questions in mind that you intend to answer. Your questions should revolve around identifying correlations and not causations. Don't worry if you don't expose an obvious correlation; your plots are successful if they identify non-correlations. 

Another common mistake is to take on a project that is only mildly interesting and without consequence or impact. For example, one might identify the most popular genre of movies without an explanation of why we should care. Perhaps there is a very good reason we should care. Don’t simply answer mild curiosities.  

## Data Description
```{admonition} Important!
:class: important
The ultimate focus of this deliverable is to **understand** your data. 
```

You will extensively document your data to illustrate that you understand it. Here are some things that you should document:  

* **Data Collection**: Explain when and how the data was collected. Explain what biases might be present in the data.  
* **Data Source**: Provide the URL where the data was collected so that Mr. Stride can download the data himself. Sometimes a site will have various fields to fill out before the data can be downloaded. These steps will not alter the URL seen in the address bar which can be confusing and add difficulty to the process of downloading the data again. Be sure you provide instructions on how to download your data.  

* **Column Descriptions**: Identify the important columns you will work with. You may have only one or two important columns. Or, perhaps you’ll have 20! Find a way to present your information in an easy to read format, such as a table. Here are things you should describe for every important column:  
    * **Name**: Provide column name as found in the file.  
    * **Description**: Give a sentence explaining what the data is. Most datasets have columns that are cryptic and hard to understand. Do not plot data that you do not understand! For example, the data might give a number representing the count of gun incidents at schools which include students inappropriately speaking about guns, pointing their fingers like a pistol, or someone complaining that they saw a police officer with a gun. Know the specific definition of your data!  
    * **Units**: Explain the units such as: dollars per year, square foot, free form human input as a string, list of words, date/time, year. State whether the data is categorical (e.g. Grade level).  
    * **Examples**: Sometimes it can be valuable to provide some examples, especially when it comes to categorical and non-numerical values. This will help you discover what type of normalization and organization is required.  
    * **Foreign Key**: If you intend to do a join with another dataset, you should list out the columns you will use to join on. It is common to have a column that is structured slightly differently from another dataset. For example, in one dataset you may have just the two letter representation of a state (e.g. WA) while in another you have the name (e.g. Washington) while in another you have odd abbreviations (e.g. Wash St). You may need to do work to normalize these columns to enable a seamless join.  
    * **Issues**: Common issues are:  
        * **Free form** human input is riddled with typos, non-conformity, difficult to summarize, and difficult to normalize. If you can’t consume the data in a way that enables you to graph it, then the data is useless.  
        * **Missing data** can be common. If the available data is scant, this can greatly skew your results and make plot creation difficult.  
        * **Errors** in the data can be rampant. Perhaps there are only a few critical errors to be aware of. For example, a column might represent inches of rain per day, but in some cases unbelievable values were used (e.g. 203.4). Discuss what validation you might execute or ways you’ll catch outliers.  
        * **Non-conformity** can destroy your ability to join tables. 

## Challenge Description
Read the list of possible challenge tasks and make sure you understand what it takes to meet the requirements of a Challenge Goal. Then, set aside ample time to completely fulfill the goal.  

Many students underestimate the amount of work to meet a Challenge. A typical mistake is to assume that they can meet the demands of "Multiple Datasets" because they have a few datasets downloaded. In reality, to qualify you must work with **four** or more datasets what require **merging** together in various ways. The datasets need to have a valid reason for merging; the merging must add value to the research.   

Others think that learning a new library will be quick and easy. They end up either not doing it at all or slapping on a piece of code that took 5-minutes to look up on the internet. The size of a student's accomplishments will impact a student's grade. Note that the amount of time spent is not graded, but it is very difficult to have a large accomplishment in a small amount of time.    

## Web Scraping
For web-scraped data, you should have at least started your attempt to scrape the data. The full collection of the data isn’t due until the next Deliverable (Organize). However, you still need to describe the data fully as you would any other dataset. 

Scraping data from a web page can get complicated due to the dynamic nature of web pages. The request API to download the HTML may not work out of the gate because the data is asynchronously loaded into the page. You should at least know if you can easily capture the data in a file. You might be able to alter the URL you download to get the data, but that can get difficult if the pages do a POST request instead of a GET. (HTTP protocol includes a “post” action where there are potentially many parameters included in the “headers” of the request.) 

You may have to manually save the HTML to a local file and then update your code to read the local file. If there are many pages to download, you may want to look into crawling a site programmatically through automation. This is wrought with potential failures and is not easy. 

In short, you cannot let web-scraping be a roadblock to your Data Science research! Find a solution early, even if it involves some manual work. Strive to understand the scope of the web scraping task; start scraping early. The more work you get done early, the better things will go for the rest of the project.  

```{admonition} Warning!
:class: warning
While using the internet to help you scrape a webpage is acceptable, you are still required to **cite** the specific source and **understand** the code in your project. To avoid uncomfortable interviews with Mr. Stride, add comments in your code that amply describe how it all works.  
```

