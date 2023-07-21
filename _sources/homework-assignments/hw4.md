# <i class="fas fa-laptop fa-fw"></i> HW4 - Education

## Overview
**Learning objective:** Apply Pandas, Seaborn, and Scikit-learn to process, visualize, and predict outcomes about data.  

## Files
* `nces-ed-attainment.csv` is a CSV file that contains the education dataset for this assessment.  
* `hw4.py` is the file for your implementations. The Run button executes this program.    
* `hw4-writeup.md` is the file for your writeup. Instead of testing, this assessment emphasizes reflection on our data analysis.  
* `cse163_imgd_NCHS.py` is a helper file that checks your plot outputs against expected output, and creates an image showing any pixel differences. (TODO: Explain how to run it. The Run button executes this program and your hw4.py.)  
* `main.py` is present simply to allow Replit Unit Tests to run.  
* `tox.ini` configures the rules enforced by `flake8`. We will eliminate some rules to hopefully make development a bit easier. Do **NOT** submit this file because your submission will be ignored during grading. Do **NOT** modify this file if you want `flake8` to pass during grading.  
* `expected` is a folder containing the expected output for `line_plot_bachelors` and `bar_chart_high_school`. Don’t modify the contents of this folder.   

## Context
The National Center for Education Statistics is a U.S. federal government agency for collecting and analyzing data related to education. We have downloaded and cleaned one of their datasets: Percentage of persons 25 to 29 years old with selected levels of educational attainment, by race/ethnicity and sex: Selected years, 1920 through 2018. The nces-ed-attainment.csv file has columns for Year, Sex, Min degree, and race/ethnicity categories.   
> Note the missing data: not all columns have data starting from 1920!  


|Year|Sex|Min degree|Total|White|Black|Hispanic|Asian|Pacific Islander|American Indian/Alaska Native|Two or more races|  
|----|---|----------|-----|-----|-----|--------|-----|----------------|-----------------------------|-----------------|
|1920|A|high school|---|22.0|6.3|---|---|---|---|---|
|1940|A|high school|38.1|41.2|12.3|---|---|---|---|---|
|⋮|⋮|⋮|⋮|⋮|⋮|⋮|⋮|⋮|⋮|⋮|
|2018|F|master's|10.7|12.6|6.2|3.8|29.9|---|---|---|


* `Year` is the year for the row. There may be more than one row for the same year to show the breakdowns by sex.  
* `Sex` is the sex of the people for the row: `F` for female, `M` for male, or `A` for all students.  
* `Min degree` is the degree of educational attainment for the row: `high school`, `associate's`, `bachelor's`, or `master's`.  
* `Total` is the overall percentage of people of the `Sex` in the `Year` with at least the `Min degree` of educational attainment.  
* `White`, `Black`, `Hispanic`, `Asian`, `Pacific Islander`, `American Indian/Alaska Native`, `Two or more races` is the percentage of students of the specified race (and of the `Sex` in the `Year`) with at least the `Min degree` of educational attainment.  

In the Charmander species, Charmander begins at stage 1, evolves into a Charmeleon at stage 2, and finally evolves into Charizard at stage 3.  

### TODO: All the below stuff needs to be deleted

### Miscellaneous Tips
As with previous assessments, you’ll also check your solutions by adding tests to `hw3_test.py` using the `assert_equals` function.
````{tab-set}
```{tab-item} Tip #1
```{admonition} Parsing
:class: hint
Here you can see examples of both parsing functions:  
* `parse`: To help test functions solved without Pandas, `cse163_utils.py` defines a `parse` function that takes a filename and returns the dataset as a list of dictionaries.   
* `read_csv`: To help test functions solved with Pandas, call `pd.read_csv` to return the dataset as a `DataFrame`.  
```python
from cse163_utils import parse
import pandas as pd

df = pd.read_csv('file.csv')
list_of_dict = parse('file.csv')
```
```{tab-item} Tip #2
```{admonition} Test Files
:class: hint
* Create your own testing CSV file and submit these files with your other files.  
* **Do not** use or introduce subdirectories (subfolders) for the test files in this assignment. Keep the file structure flat.  
* When specifying file names, use **relative** paths, such as `pd.read_csv('pokemon_test.csv')`.  
* **Do not** use the `pokemon_box.csv` file in your own test cases. The file is too large to come up with the correct answer on your own; it’s not valid to assume your code's output is the correct answer and to blindly use that as the expected value.  
```
```{tab-item} Tip #3
```{admonition} Test Methods
:class: hint
* Write at least one test function for each problem and give it a descriptive name that indicates the function being tested, such as `test_species_count`.  
* In addition to the provided `pokemon_test.csv` example file, add at least 2 (**two**) additional test files (one file for each case you're testing). These data files contain short, contrived, targeted data that is easy to verify in your tests.  
* One test function per problem is fine since both ways of solving the problem should compute the same result. In other words, you may choose to write one method, `test_species_count` that tests both the manual and pandas code.  
```
```{tab-item} Tip #4
```{admonition} Constants, Globals & Locality
:class: hint
* Do **NOT** use globals in your test file. Instead, use constants or method parameters.   
* Don't make "heavy weight" constants. (See: <a href="https://courses.cs.washington.edu/courses/cse163/22sp/resources/code_quality/#constant-names" target="_blank">Code Quality - Constants</a> for more details.)  
* Attempt to keep declarations and values in close proximity to where they are used. This helps the reader understand the code better. This means, define expected values in the method where they are used.  
* Attempt to reduce redundancy with code instead of copy/paste. But, in test files, some redundancy is allowed so that tests can remain insulated from one another and to improve readability of individual test functions.   

Here is some sample code:  
```python
'''
This is my test file
'''
import pandas as pd
import hw3_manual
import hw3_pandas

from cse163_utils import parse

# do NOT use globals like these
test_data_1_dict = parse('pokemon_box.csv')
test_data_1_df = pd.read_csv('pokemon_box.csv')

# these are constants and are fine to use if you want
FILE_1 = 'test_data1.csv'
FILE_2 = 'test_data2.csv'

def test_example():
    '''
    Test the method example using both manual and pandas
    '''
    # test simple case
    expected = {'age':15, 'height':102}
    assert_equals(expected, hw3_pandas.example(pd.read_csv(FILE_1)))
    assert_equals(expected, hw3_manual.example(parse(FILE_1)))

    # test extreme case
    expected = {'age':99, 'height':999}
    assert_equals(expected, hw3_pandas.example(pd.read_csv(FILE_2)))
    assert_equals(expected, hw3_manual.example(parse(FILE_2)))

    # test redundant case
    expected = {'age':2, 'height':25}
    assert_equals(expected, hw3_pandas.example(pd.read_csv('test_data3.csv')))
    assert_equals(expected, hw3_manual.example(parse('test_data3.csv')))


def main():
    # be sure to call every test you write
    test_example()


if __name__ == '__main__':
    main()
```
````


## Required Methods
In the file named `hw3.py`, implement six methods: `species_count`, `max_level`, `filter_range`, `mean_attack_for_type`, `count_types`, 
and `mean_attack_per_type`. The description for each method is found in the tabs below.   

For each method described in the tabs you must: 
* <i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_manuals.py` the function as described in the tabs.  
* <i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_pandas.py` the same function using Pandas. Rather than take a list of dictionaries, the Pandas version will take a `DataFrame` argument.   
* <i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_test.py` one or more test functions that call the method with various input. Compare the actual results to the expected results using `assert_equals`. Do **not** do all your testing with the `pokemon_test.csv` file; be sure to add 2 (**two**) additional test cases by creating your own CSV files. (See Miscellaneous Tip #4 above.)

```{admonition} Challenge
:class: note
Way down below is a challenge question which is optional and not graded. See the <a href="#challenge-question">Challenge Question</a> section down below for details.
```

````{tab-set}
```{tab-item} species_count
<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_manual.py` a function `species_count` that takes a parsed pokemon dataset and returns the number of unique pokemon species in the dataset as determined by the `name` attribute without using Pandas.

For the `pokemon_test.csv` file, `species_count(data)` should return `3`.

```{admonition}  Do not use id
:class: important
Do not use the `id` attribute to solve this this problem. Instead, you use the `name` attribute.  
I realize that `id` should be the right approach, but UW has other ideas here. Don't fight it. Just use `name`.
```

```{tab-item} max_level
<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_manual.py` a function `max_level` that takes a parsed pokemon dataset and returns a 2-element tuple of the `(name, level)` of the pokemon with the highest `level` in the dataset. If there is more than one pokemon with the highest `level`, return the pokemon that appears first in the file.

For the `pokemon_test.csv` file, `max_level(data)` should return the 2-element tuple, `('Lapras', 72)`.

```

```{tab-item} filter_range
<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_manual.py` a function `filter_range` that takes a parsed pokemon dataset and  two numbers: a lower bound (inclusive) and upper bound (exclusive). The function returns a list of the names of pokemon whose `level` fall within the bounds in the same order that they appear in the dataset.

For the `pokemon_test.csv` file, `filter_range(data, 35, 72)` should return `['Arcanine', 'Arcanine', 'Starmie']`. Note that Lapras is not included because the upper bound is exclusive of Lapras, which is exactly level 72.

```{admonition} Series to list
:class: hint
To convert a Pandas Series to a list, use the built-in list function. For example:  
```python
# data is a DataFrame storing following info:
# name,age,species
# Fido,4,dog
# Meowrty,6,cat
# Chester,1,dog
# Phil,1,axolotl
names = data['name']  # Series
list(names)  # ['Fido', 'Meowrty', 'Chester', 'Phil']
row = data.loc[1]  # Series
list(row)  # ['Meowrty', 6, 'cat']
```
```{tab-item} mean_attack_for_type
<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_manual.py` a function `mean_attack_for_type` that takes a parsed pokemon dataset and a string representing the pokemon `type`. The function returns the average `atk` for all the pokemon in the dataset with the given `type`. If there are no pokemon of the given `type`, return `None`.

For the `pokemon_test.csv` file, `mean_attack_for_type(data, 'fire')` should return `47.5`.
```
```{tab-item} count_types
<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_manual.py` a function `count_types` that takes a parsed pokemon dataset and returns a dictionary representing for each pokemon `type` the number of pokemon of that `type`. The order of the keys in the returned dictionary does not matter.

For the `pokemon_test.csv` file, `count_types(data)` should return `{'fire': 2, 'water': 2}`.

```{admonition} Series to dict
:class: hint
To convert a Pandas Series to a dictionary, use the built-in `dict` function. The dictionary keys are determined by the series index. For example:  
```python
# data is a DataFrame storing following info:
# name,age,species
# Fido,4,dog
# Meowrty,6,cat
# Chester,1,dog
# Phil,1,axolotl
names = data['name']  # Series
dict(names)  # {0: 'Fido', 1: 'Meowrty', 2: 'Chester', 3: 'Phil'}
row = data.loc[1]  # Series
dict(row)  # {'name': 'Meowrty', 'age': 6, 'species': 'cat'}
```
```{tab-item} mean_attack_per_type
<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_manual.py` a function `mean_attack_per_type` that takes a parsed pokemon dataset and returns a dictionary representing for each pokemon `type` the average `atk` of pokemon of that `type`. The order of the keys in the returned dictionary does not matter.

For the `pokemon_test.csv` file, `mean_attack_per_type(data)` should return `{'fire': 47.5, 'water': 140.5}`.

```
````

## Code Quality
Assessment submissions should pass these checks: `flake8`, and <a href="https://courses.cs.washington.edu/courses/cse163/22sp/resources/code_quality/" target="_blank">code quality guidelines</a>. The code quality guidelines are very thorough. For this assessment, the most relevant rules can be found in these sections, with the **bolded** one being new from the last homework:  

* <a href="https://courses.cs.washington.edu/courses/cse163/22sp/resources/code_quality/#naming-conventions" target="_blank">Naming</a>  
* <a href="https://courses.cs.washington.edu/courses/cse163/22sp/resources/code_quality/#documentation" target="_blank">Documentation</a>   
* <a href="https://courses.cs.washington.edu/courses/cse163/22sp/resources/code_quality/#efficiency-and-redundancy" target="_blank">Efficiency and Redundancy</a>  
    * Boolean Zen  
    * Loop Zen  
    * Factoring   
    * Unnecessary Cases
    * **Avoid Looping with Pandas**

```{admonition} Reminder
:class: important
Make sure to provide a descriptive comments in doc-string format.
```  
## Rubric
Rubric information can be found in the instruction in the Replit project.   

## Challenge Question

**OPTIONAL**: This challenge question is not graded and is here for those students who already know Python and want to flex some of their intellectual muscle.  
**NOTE**: If you implement this challenge question, you'll need to document all methods fully with doc-strings so that all the grading scripts pass. You don't want to have your grade drop!  Be sure to test it, too!  
* * * 
<i class="fas fa-pen-square fa-fw"></i> **Write** a class named `MyStats` inside the file `hw3_manual.py`. It will implement
several methods to support the required functionality. The `class` will have a static method named `compute` that will calculate three
statistics using Python libraries; do not implement the calculations yourself.  

Here are the three relatively esoteric statistics that the `compute` method provides:  
1) **Kurtosis**: Kurtosis is a measure of the tailedness or shape of a probability distribution. It quantifies whether the distribution has heavy tails or is more peaked compared to a normal distribution. You can calculate the kurtosis using the `scipy.stats.kurtosis` function.   
2) **Skewness**: Skewness measures the asymmetry of a probability distribution. It indicates whether the distribution has a longer tail on one side compared to the other. Positive skewness means the tail is on the right side, while negative skewness means the tail is on the left side. You can calculate the skewness of a distribution using the `scipy.stats.skew` method.  
3) **95th Percentile**: Numpy provides a convenient way to calculate percentiles. A percentile represents the values below which a given percentage of the data falls. For example, the 50th percentile is the median. Numpy's percentile function allows you to calculate percentiles easily for a given list of numbers. You will calculate the 95th percentile.

Here is sample code that shows how client code can use the class:  
```python
'''
This file is named: my_client.py
'''
# import the MyStats class from the file that implements it
from hw3_manual import MyStats

# Sample list on which to calculate three stats
l = [1, 2, 3, 4, 5, 6, 7, 10, 15]

# unpack the three statistics directly from the method call
a, b, c = MyStats.compute(l)

# store the results object (which is of type MyStats) from the method call
obj = MyStats.compute(l)

# print the object directly
print(obj) # prints: MyStats(kertosis=0.10, skew=0.98, 95_percentile=13.00)

# print the three unpacked statistics (raw & unrounded)
print(a, b, c)

# iterate the object and print each stat rounded to 3 decimal places
for s in obj:
    print(f'Stat = {s:.3f}')
```
The expected output of the above code is:  
```
MyStats(kertosis=0.10, skew=0.98, 95_percentile=13.00)
0.10378287249864737 0.9838565052198887 12.999999999999998
Stat = 0.104
Stat = 0.984
Stat = 13.000
```
Several higher Object Oreinted pieces of functionality are are present. You need to figure them out.  
```{admonition} Tips
:class: hint
* Mr. Stride's implementation was a total of 20 lines of code (including imports and empty lines, but excluding comments).   
* Use an <a href="https://docs.python.org/3/library/functions.html#staticmethod" target="_blank">annotation</a> to designate `compute` to be a static method.  
* Use <a href="https://docs.python.org/3/reference/datamodel.html#special-method-names" target="_blank">special methods</a> to allow the object to be _iterable_ and _printable_.  
* Consider leveraging a list's inherent ability to be _iterable_ to simpify the object's required implementation.  
* Follow privacy rules by using Python's naming conventions (using underscores) for private instance field names.   
```
