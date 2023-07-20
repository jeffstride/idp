# <i class="fas fa-laptop fa-fw"></i> HW5 - Search Engine

## Overview
**Learning objective:** Implement specialized data types with Python classes for tf-idf information retrieval.  

## Files
* `search_engine.py` is the file representing the SearchEngine class as well as a command-line interface for using the SearchEngine.  
* `document.py` is the file representing a single document in the SearchEngine.  
* `hw5_test.py` is the file for you to put your own tests. The Run button executes this program.  
* `server.py` and `index.html` provide a web app for you to run your completed search engine. You do not need to look at or modify these files ever.  
* `cse163_utils.py` is a helper file that has code to help you test your code.    

```{admonition} Time Management
:class: warning
This assessment is very information-dense. Plan ahead by taking notes of what you need to do and where you will need to do it. It will probably help to get a global view of the entire assessment by reading **ALL** of the components before starting any coding—we expect students to spend at least 40 minutes reading, synthesizing, and planning before starting any coding.
```

```{admonition} Video on TF-IDF
:class: seealso
Watch the video of [Hunter Schafer](https://www.loom.com/share/118366e8ba1a427dad84870b869b660a?sid=d7353687-52cf-4ab3-a737-ed743bed0971).
```

## 
A search engine is an algorithm that takes a query and retrieves the most relevant documents for that query. In order to identify the most relevant documents, our search engine will use term frequency–inverse document frequency (tf–idf), a text information statistic for determining the relevance of a term to each document from a corpus consisting of many documents.

The tf-idf statistic consists of two components: term frequency and inverse document frequency. Term frequency computes the number of times that a term appears in a document (such as a single Wikipedia page). If we were to use only the term frequency in determining the relevance of a term to each document, then our search result might not be helpful since most documents contain many common words such as “the” or “a”. In order to down-weight these common terms, the document frequency computes the number of times that a term appears across the corpus of all documents. The tf-idf statistic takes a term and a document and returns the term frequency divided by the document frequency.

In this assessment, we’ll implement two classes: a `Document` class to represent individual web pages and a `SearchEngine` class that aggregates the corpus of all `Document` objects. The `SearchEngine` builds on the `Document`, so be sure to fully complete the `Document` class before moving onto the `SearchEngine`.