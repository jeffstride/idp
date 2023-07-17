# <i class="fas fa-laptop fa-fw"></i> HW3 - Pokémon



## Overview
**Learning objective:** Read, process, and group CSV data to compute descriptive statistics with and without Pandas.  

## Files
* `hw3_manual.py` is the file for you to put your implementations for solving each problem without Pandas.  
* `hw3_pandas.py` is the file for you to put your implementations for solving each problem with Pandas.  
* `hw3_test.py` is the file for you to put your own tests. You need to change `.replit` to run your tests. Be sure to use the _main-pattern_ for this file. Make sure it runs successfully!  
* `cse163_utils.py` is a helper file that has code to help you test your code.  
* `pokemon_box.csv` is a large CSV file that stores information about pokemon.  
* `pokemon_test.csv` is a very small CSV file that stores information about pokemon used for the example cases.  
* `hw3.py` is the file to put your implementations for each problem. `hw3.py` is not a runnable program, so we don’t use the _main-method_ pattern.  

## Context
In the <a href="https://en.wikipedia.org/wiki/Pok%C3%A9mon" target="_blank">Pokémon</a> video game series, the player catches pokemon, fictional creatures trained to battle each other as part of a sport franchise. Pokémon exerted significant cultural influence on people who grew up in the late 1990s and early 2000s not only in its country of origin, Japan, but also around the world. More recently,
<a href="https://en.wikipedia.org/wiki/Pok%C3%A9mon_Go" target="_blank"> Pokémon Go</a> became a viral hit as hundreds of millions of people played the augmented-reality game at its peak during the summer of 2016. You do not need to understand the details of Pokémon or need to have played the game to do the assignment. All you need to understand is the statistics we provide in our dataset about each pokemon.  

The `pokemon_box.csv` file stores some imagined data about a player’s pokemon in the following format.  

|id|name|level|personality|type|weakness|atk|def|hp|stage|  
|--|----|-----|-----------|----|--------|---|---|--|-----|
|1|Bulbasaur|12|Jolly|Grass|Fire|45|50|112|1|

* `id` is a unique numeric identifier corresponding to the species of a pokemon. All pokemon of the same species share the same id.  
* `name` is the name of the species of pokemon, such as Bulbasaur.  
* `level` is the integer level of the pokemon.  
* `personality` is a one-word string describing the personality of the pokemon, such as Jolly.  
* `type` is a one-word string describing the type of the pokemon, such as Grass.  
* `weakness` is the enemy type that this pokemon is weak toward. Bulbasaur is weak to fire-type pokemon.  
* `atk`, `def`, `hp` are integers that indicate the attack power, defense power, and hit points of the pokemon.  
* `stage` is an integer that indicates the particular developmental stage of the pokemon.  

In the Charmander species, Charmander begins at stage 1, evolves into a Charmeleon at stage 2, and finally evolves into Charizard at stage 3.  

![Charmander stages](https://courses.cs.washington.edu/courses/cse163/22sp/assets/images/pokemon.png)  

The problems in this assessment focus on providing <a href="https://en.wikipedia.org/wiki/Descriptive_statistics" target="_blank">descriptive statistics</a> for summarizing the pokemon dataset, such as computing the mean or count of a certain column. Solve each problem in two ways.  

### Without Pandas
Use Python built-in data structures plus Python math functions to solve the problems in the file `hw3_manual.py`. These 6 functions take a list of dictionaries representing the parsed pokemon dataset.

```python
data = parse('pokemon_box.csv')

print('Number of species:', hw3_manual.species_count(data))
print('Highest level pokemon:', hw3_manual.max_level(data))
print('Low-level Pokemon:', hw3_manual.filter_range(data, 1, 9))
print('Average attack for fire types:', hw3_manual.mean_attack_for_type(data, 'fire'))
print('Count of each Pokemon type:')
print(hw3_manual.count_types(data))
print('Average attack for each Pokemon type:')
print(hw3_manual.mean_attack_per_type(data))
```

### With Pandas
Use Pandas (plus Python math functions) in `hw3_pandas.py`. **Do not use any loops or list/dictionary comprehensions.** These 6 functions take a Pandas `DataFrame` representing the parsed pokemon dataset.

```python
data = pd.read_csv('pokemon_box.csv')

print('Number of species:', hw3_pandas.species_count(data))
print('Highest level pokemon:', hw3_pandas.max_level(data))
print('Low-level Pokemon:',  hw3_pandas.filter_range(data, 1, 9))
print('Average attack for fire types:', hw3_pandas.mean_attack_for_type(data, 'fire'))
print('Count of each Pokemon type:')
print(hw3_pandas.count_types(data))
print('Average attack for each Pokemon type:')
print(hw3_pandas.mean_attack_per_type(data))
```
```{admonition} You May Assume
:class: hint
Assume the data is never empty (there’s at least one pokemon) and that there’s no missing data (each pokemon has every attribute).
```
```{admonition} Do NOT Assume
:class: warning
Canonically, Pokémon cannot have an attack stat of 0. For this assessment, however, you should NOT make that assumption.
```
### Miscellaneous Tips
As with previous assessments, you’ll also check your solutions by adding tests to `hw3_test.py` using the `assert_equals` function.
````{tab-set}
```{tab-item} Tip #1
```{admonition} Parsing
:class: hint
You can see examples of both lf these parsing functions below:  
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
* **Do not** use introduce subdirectories (subfolders) for the test files in this assignment. Keep the file structure flat.  
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
```{admonition} Globals & Locality
:class: hint
* Do **NOT** use globals in your test file. Instead, use constants or method parameters.   
* Attempt to keep declarations and values in close proximity to where they are used. This helps the reader understand the code better. This means, define expected values in the method where they are used.  
* Attempt to reduce redundancy with code instead of copy/paste.  

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
In the file named `hw3.py`, implement six methods: `species_count`, `max_level`, `filter_range`, `mean_attack_for_type`, `count_types`,  and `mean_attack_per_type`. The description for each
method is found in the tabs below.   

You are required to **TEST** each method. Each test method should include the example provided herein.  

Way down below is a challenge question which is optional and not graded. See the <a href="#challenge-question">Challenge Question</a> section down below for details.

````{tab-set}
```{tab-item} species_count
<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_manual.py` a function `species_count` that takes a parsed pokemon dataset and returns the number of unique pokemon species in the dataset as determined by the `name` attribute without using Pandas.

For the `pokemon_test.csv` file, `species_count(data)` should return `3`.

<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_pandas.py` the same function using Pandas. Rather than take a list of dictionaries, this takes a Pandas `DataFrame`.

<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_test.py` one or more test functions that call `species_count` with some CSV files and compares the output of the program with the expected value using `assert_equals`. In addition to the `pokemon_test.csv` file, add two additional test cases by creating your own CSV files.

```{admonition}  Do not use `id`
:class: important
Do not use the `id` attribute to solve this this problem. Instead, you use the `name` attribute.  
I realize that `id` should be the right approach, but UW has other ideas here. Don't fight it. Just use `name`.
```

```{tab-item} max_level
<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_manual.py` a function `max_level` that takes a parsed pokemon dataset and returns a 2-element tuple of the `(name, level)` of the pokemon with the highest `level` in the dataset. If there is more than one pokemon with the highest `level`, return the pokemon that appears first in the file.

For the `pokemon_test.csv` file, `max_level(data)` should return the 2-element tuple, `('Lapras', 72)`.

<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_pandas.py` the same function using Pandas. Rather than take a list of dictionaries, this takes a Pandas `DataFrame`.

<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_test.py` one or more test functions that call `max_level` with some CSV files and compares the output of the program with the expected value using `assert_equals`. In addition to the `pokemon_test.csv` file, add two additional test cases by creating your own CSV files.

```

```{tab-item} filter_range
<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_manual.py` a function `filter_range` that takes a parsed pokemon dataset and  two numbers: a lower bound (inclusive) and upper bound (exclusive). The function returns a list of the names of pokemon whose `level` fall within the bounds in the same order that they appear in the dataset.

For the `pokemon_test.csv` file, `filter_range(data, 35, 72)` should return `['Arcanine', 'Arcanine', 'Starmie']`. Note that Lapras is not included because the upper bound is exclusive of Lapras, which is exactly level 72.

<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_pandas.py` the same function using Pandas. Rather than take a list of dictionaries, this takes a Pandas `DataFrame`.

<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_test.py` one or more test functions that call `max_level` with some CSV files and compares the output of the program with the expected value using `assert_equals`. In addition to the `pokemon_test.csv` file, add two additional test cases by creating your own CSV files.

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

For the pokemon_test.csv file, `mean_attack_for_type(data, 'fire')` should return `47.5`.

<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_pandas.py` the same function using Pandas. Rather than take a list of dictionaries, this takes a Pandas `DataFrame`.

<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_test.py` one or more test functions that call `max_level` with some CSV files and compares the output of the program with the expected value using `assert_equals`. In addition to the `pokemon_test.csv` file, add two additional test cases by creating your own CSV files.
```
```{tab-item} count_types
<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_manual.py` a function `count_types` that takes a parsed pokemon dataset and returns a dictionary representing for each pokemon `type` the number of pokemon of that `type`. The order of the keys in the returned dictionary does not matter.

For the `pokemon_test.csv` file, `count_types(data)` should return `{'fire': 2, 'water': 2}`.

<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_pandas.py` the same function using Pandas. Rather than take a list of dictionaries, this takes a Pandas `DataFrame`.

<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_test.py` one or more test functions that call `max_level` with some CSV files and compares the output of the program with the expected value using `assert_equals`. In addition to the `pokemon_test.csv` file, add two additional test cases by creating your own CSV files.

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

<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_pandas.py` the same function using Pandas. Rather than take a list of dictionaries, this takes a Pandas `DataFrame`.

<i class="fas fa-pen-square fa-fw"></i> **Write** in `hw3_test.py` one or more test functions that call `max_level` with some CSV files and compares the output of the program with the expected value using `assert_equals`. In addition to the `pokemon_test.csv` file, add two additional test cases by creating your own CSV files.
```
````

## Code Quality
Assessment submissions should pass these checks: `flake8`, and <a href="https://courses.cs.washington.edu/courses/cse163/22sp/resources/code_quality/" target="_blank">code quality guidelines</a>. The code quality guidelines are very thorough. For this assessment, the most relevant rules can be found in these sections:  

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

**OPTIONAL**: This challenge method is not graded and is here for those students who already know Python and want to flex some of their intellectual muscle.  
**NOTE**: If you implement this method, you'll need to document all methods fully with doc-strings so that all the grading scripts pass. You don't want to have your grade drop!  Be sure to test it, too!  

<i class="fas fa-pen-square fa-fw"></i> **Write** a class named `xx` inside the file `hw3_manual.py`. It will implement
several methods to support the primary functionality. 

<i class="fas fa-pen-square fa-fw"></i> **Write** a method named `compute` that will take a DataFrame as an argument. It will computer three statistics about the data frame (described below). The method will return the appropriate "thing" that allows the method to be called in two different ways. (See code sample below)  

* stat1:  
* stat2:  
* stat3:  

📝 **TIP**: To enable the return value to be unpacked (as shown in the example below), implement the correct special methods using the underscore syntax. For example: `def __init__()`.
```python
# get our dataframe of data
df = pd.read_csv('data.csv')
# create an instance of our class
x = xx()
# unpack the results into three separate statistics
stat1, stat2, stat3 = x.compute(df)
print(f's1: {stat1} s2: {stat2} s3: {stat3}')
# alternatively, use the return object
result = x.compute(df)
print(f's1: {result.get_stat1()} s2: {result.get_stat2()} s3: {result.get_stat3()}')
```


```{admonition} Tips
:class: hint
* Follow privacy rules by using Python's naming conventions for private instance fields 
* Something else.. 
```

