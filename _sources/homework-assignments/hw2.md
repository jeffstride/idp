# <i class="fas fa-laptop fa-fw"></i> HW2 - Primer



## Overview
**Learning objective:** Apply control structures and data structures to solve problems involving numbers, text, and files.

## Files
* `hw2.py` is the file to put your implementations for each problem. hw1.py is not a runnable program, so we don’t use the main-method pattern.  
* `hw2_test.py` is the file for you to put your own tests. The Run button executes this program.  
* `cse163_utils.py` is a helper file that has code to help you test your code.  

```{admonition} Expectation!
:class: important
In hw2.py you should not use any `import` statements or features in Python we have not yet discussed in class, online book, or in homework handout. All of these problems should be solved using the fundamental constructs we’ve learned in class so far. For your testing program, you can use imports. In fact, you're expected to use cse163_utils‘ `assert_equals` function.
```

* * * 
## Required Methods
In the file named `hw2.py`, implement seven methods: `count_divisible_digits`, `is_relatively_prime`, `travel`, `reformat_date`, `longest_word`,  `get_average_in_range` and `mode_digit`. The description for each
method is found in the tabs below.   

You are required to **TEST** each method. Each test method should include the example method calls provided herein.  

Way down below is a challenge question which is optional and not graded. See the <a href="#challenge-question">Challenge Question</a> section down below for details.

````{tab-set}
```{tab-item} count_divisible_digits
 <i class="fas fa-pen-square fa-fw"></i> **Write** a function `count_divisible_digits` that takes two integer numbers `n` and `m` as arguments and returns the number of digits in n that are divisible by m. If m is 0, then count_divisible_digits should return 0. For this problem, any digit in n that is 0 is divisible by any number. You may assume m is a single digit (0 ≤ m <10) and that it is not negative.

<i class="fas fa-pen-square fa-fw"></i> **Write** a test in the file `hw2_test.py` that calls the function with some inputs and compares the output of the program with the expected value using assert_equals. Include test cases for all of the examples above as well as 3 (**three**) additional test cases.  

Here are some examples that you should make sure appear in `hw2_test.py`:  
| call | returns | comments |
|------|---------|----------|
|count_divisible_digits(650899, 3)| 4| The four digits 0, 6, and 9 are all divisible by 3|  
|count_divisible_digits(-204, 5)|1| Only 0 is divisible by 5|  
|count_divisible_digits(24, 5)| 0| No digit is divisible by 5|   
|count_divisible_digits(1, 0) |0| When `m=0`, return zero.|  

```{admonition}  Do Not Use String
:class: important
Do not use `str` to solve any part of this this problem in any way. Instead, you should solve this problem by manipulating the number itself using integer division. Recall that:  
* `n // 10` evaluates to all but the last digit of n.  
* `n % 10` evaluates to the last digit of n.  
```

```{tab-item} is_relatively_prime
 <i class="fas fa-pen-square fa-fw"></i> **Write** a function `is_relatively_prime` that takes two integer numbers `n` and `m`, returning `True` if `n` and `m` are relatively prime to each other and `False` otherwise. Two numbers are relatively prime if they share no common factors besides 1. (1 is relatively prime with every number.) Assume the value of `n` and `m` are at least one. 

 <i class="fas fa-pen-square fa-fw"></i> **Write** a test that calls the function with some inputs and compares the output of the program with the expected value using `assert_equals`. Include test cases for all of the examples below as well as 3 (**three**) additional test cases:  

Here are some examples that you should make sure appear in `hw2_test.py`:  
| call | returns | comments |
|------|---------|----------|
|is_relatively_prime(12, 13)| True| The factors of 12 are 1, 2, 3, 4, 6, 12 and the factors of 13 are 1, 13.|  
|is_relatively_prime(12, 14)|False| The factors of 12 are 1, 2, 3, 4, 6, 12 and the factors of 14 are 1, 2, 7, 14.|  
|is_relatively_prime(5, 9)| True| The factors of 5 are 1, 5 and the factors of 9 are 1, 3, 9.|   
|is_relatively_prime(8, 9) |True| The factors of 8 are 1, 2, 4, 8 and the factors of 9 are 1, 3, 9.|  
|is_relatively_prime(8, 1) |True| We define that 1 is relatively prime with every number.|  

```{admonition} No Data Structures  
:class: important
**Do not** use data structures to store factors during the execution of the algorithm. Also, use a single loop rather than nested loops.

```

```{tab-item} travel
<i class="fas fa-pen-square fa-fw"></i> **Write** a function `travel` which takes a string of north, east, south, west directions, a starting location on a grid `x`, and a starting location on a grid `y`. Your function should return a tuple that indicates the new position after following the directions starting from the given `x`, `y`. The returned tuple should be in the format `(x_new, y_new)`.

The directions string will use `'N'` to indicate increasing the y-coordinate, `'E'` to indicate increasing the x-coordinate, `'S'` to indicate decreasing the y-coordinate, and `'W'` to indicate decreasing the x-coordinate. The case of the characters should be ignored. You can assume that `x` and `y` are both of type `int`. Any characters that are not 'N', 'E', 'W', or 'S' (ignoring letter-casing) should be ignored.

`travel('NW!ewnW', 1, 2)` should return the tuple `(-1, 4)` following this sequence of movements:
1. Start at (1, 2).  
2. Move 'N' to (1, 3).  
3. Move 'W' to (0, 3).  
4. Ignore '!' since it is not a valid direction.  
5. Move 'e' to (1, 3).  
6. Move 'w' to (0, 3).  
7. Move 'n' to (0, 4).  
8. Move 'W' to (-1, 4).  

<i class="fas fa-pen-square fa-fw"></i> **Write** a test that calls the function with some inputs and compares the output of the program with the expected value using `assert_equals`. Include test cases for the example above as well as 3 (**three**) additional test cases.

```
```{tab-item} reformat_date
<i class="fas fa-pen-square fa-fw"></i> **Write** a function `reformat_date` which takes three strings as arguments representing a date, a current date format, and a target date format and returns a new string with the date formatted in the target format.  

For example, if we made the method call,  `reformat_date("12/31/1998", "M/D/Y", "D/M/Y")` it should return the string `"31/12/1998"`. In this example, the first argument represents a date and the second argument specifies this date is currently in the format Month/Day/Year (abbreviated `"M/D/Y"`). The third argument specifies that the method should return a new date in the format of Day/Month/Year format (abbreviated `"D/M/Y"`).  

A date string will be some non-empty string of numbers separated by `/` (e.g, `"3/6/1995"`). Note that the numbers between the `/`‘s can have any number of digits, but you may assume there is at least one digit for each part of the date provided.  

The current and target formats will be some non-empty sequence of the characters `'D'`, `'M'`, `'Y'` separated by `/`. You can assume the given date and the current format will match up (i.e., they will have the same number of `/`‘s) and that any date symbol that appears in the target format also appears in the current format (i.e., if the target format contains a `'Y'` the current format will also contain a `'Y'`).  

Below are some valid/invalid examples of current and target formats. You do **not** need to handle invalid formats. You may assume we will never pass you an example that is invalid. Make sure these valid test cases appear in `hw2_test.py`:
| call | returns | notes |  
|------|---------|-------|  
|`reformat_date("1/2/3", "M/D/Y", "Y/M/D")`|`"3/1/2"`| Valid |   
|`reformat_date("0/200/4", "Y/D/M", "M/Y")`|`"4/0"`| Valid |  
|`reformat_date("3/2", "M/D", "D")`|`"2"`| Valid |  
|`reformat_date("3/2", "M/D/Y", "Y/M/D")`| | Invalid - Date & Format do not match |  
|`reformat_date("3/2", "M/D", "Y/M/D")`| | Invalid - Current Format missing 'Y' |  
|`reformat_date("1/2/3/4", "M/D/Y/S", "M/D")`| | Invalid - Date format contains 'S'|  
|`reformat_date("", "", "")`| | Invalid - empty string|  

<i class="fas fa-pen-square fa-fw"></i> **Write** a test that calls the function with some inputs and compares the output of the program with the expected value using `assert_equals`. Include test cases for the example above as well as 3 (**three**) additional test cases.

Again, you may assume **we won’t pass you any of these invalid date formats**. We wanted to provide this list and rationale for why they are invalid to give you a better sense of what assumptions you can make about your inputs.

```{admonition} Implementation
:class: tip
Your function should be as general as possible and avoid hard-coding specific orderings of the date parts.
```
```{tab-item} longest_word
<i class="fas fa-pen-square fa-fw"></i> **Write** a function `longest_word` that takes a string filename 
and returns the longest word in the file with which line it appears on. A word here is defined as a 
sequence of characters separated by whitespace. If there are ties for the longest word, it should 
return the one that appears first in the file. If the file is empty or there are no words in the file, 
the function should return `None`. You may assume that the file exists. 

<i class="fas fa-pen-square fa-fw"></i> **Write** a test that calls the `longest_word` with some file names and compares the 
output of the method with the expected value using `assert_equals`. Include the test case below as well as 3 (**three**) 
additional test cases.  

📝 **TIP**: Each test case should have a test file that you have created. Be sure that you **submit** these
test files with your python files.  Your test need to run successfully!!   

Using the file contents below, the call `longest_word('song.txt')` should return `'3: Merrily,'`, the first
word in the third line of the file shown here. Note that the filename uses a relative path.   
```{admonition} song.txt
Row, row, row your boat  
Gently down the stream   
Merrily, merrily, merrily, merrily  
Life is but a dream!  
```
```{tab-item} get_average_in_range
<i class="fas fa-pen-square fa-fw"></i> **Write** a function `get_average_in_range` that takes a list of integers, an integer
`low`, and an integer `high`, and returns the average of all values within the list that lies in the given range from `low`
(inclusive) to `high` (exclusive). If there are no values in the given range, returns `0`.


Here are some examples that you should make sure appear in `hw2_test.py`:  

| call | returns | notes |  
|------|---------|-------| 
|`get_average_in_range([1, 5, 6, 7, 9], 5, 7)`| `5.5`|only 5 and 6 fall in the range between 5 (inclusive) and 7 (exclusive), and the average of 5 and 6 is 5.5.|  
|`get_average_in_range([1, 2, 3], -1, 10)`|`2.0`| 1, 2, 3 all fall within the specified range and the average of the three numbers is 2.0.|  

<i class="fas fa-pen-square fa-fw"></i> **Write** a test that calls the `get_average_in_range` with some inputs and compares the 
outputs of the method with the expected value using `assert_equals`. Include the test cases above as well as 3 (**three**) 
additional test cases.   
```
```{tab-item} mode_digit
<i class="fas fa-pen-square fa-fw"></i> **Write** a function `mode_digit` that takes an integer number `n` and returns 
the digit that appears most frequently in that number. The given number may be positive or negative, but the most 
frequent digit returned should always be non-negative. If there is a tie for the most frequent digit, the digit with 
the greatest value should be returned.  

Here are some examples that you should make sure appear in `hw2_test.py`:  

| call | returns | notes |  
|------|---------|-------|  
|`mode_digit(12121)`|`1`|1 appears the most--three times|  
|`mode_digit(0)`|`0`|Zero can be thought of as a special case|  
|`mode_digit(-122)`|`2`|Negative numbers can be tricky!|  
|`mode_digit(1211232231)`|`2`|Both 1 & 2 appear 4 times, but 2 &gt; 1|  

<i class="fas fa-pen-square fa-fw"></i> **Write** a test that calls the `mode_digit` with some inputs and compares the 
outputs of the method with the expected value using `assert_equals`. Include the test cases above as well as 3 (**three**) 
additional test cases.   

```{admonition} Requirements
:class: important  
* Do not create strings in any way to solve any part of the problem.  
* Do not use any nested loops or recursion.  
* Do not use an if, elif, or else branch for each digit.  
📝 **TIP**: Use data structures to count digit occurrences.  
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

```{admonition} Requirements
:class: important
Make sure to provide a descriptive file header in doc-string format, not something generic like “implements functions for Primer”.
```  
## Rubric
Rubric information can be found in the instruction in the Replit project.   

## Challenge Question

**OPTIONAL**: This challenge method is not graded and is here for those students who already know Python and want to flex some of their intellectual muscle.  
**NOTE**: If you implement this method, you'll need to document all methods fully with doc-strings so that all the grading scripts pass. You don't want to have your grade drop!  Be sure to test it, too!  

<i class="fas fa-pen-square fa-fw"></i> **Write** a function named `weighted_average` that will take two `numpy` arrays.
The first argument, `values` will be a two-dimensional array (of any number of rows & cols) that contains real values. The second argument, 
`weights`, will be a one-dimensional array with the same number of elements as there are cols in the argument `values`. 
The method will return a weighted average of all the values using the weights across each row. Here are some examples:    

```python
# use these numpy arrays for the calls in the table below
v1 = np.array([[1],[2]])  # 2x1 array
w1 = np.array([3])

v2 = np.array([[1, 2, 3],[4, 3, 4]]) # 2x3 array
w2 = np.array([1, 0, 1])

v3 = np.array([[1, 2, 3, 0],[4, 5, 6, 1],[7, 8, 9, 2]]) # 3x4 array
w3 = np.array([0, 0, 0, 2])
```

| call | returns | notes |  
|------|---------|-------|  
|`weighted_average(v1, w1)`|`4.5`| $(3*1 + 3*2)/2 = 4.5$|  
|`weighted_average(v2, w2)`|`2.0`|$(1*1 + 2*0 +3*1 + 4*1 + 3*0 + 4*1)/6 = 2.0$|  
|`weighted_average(v3, w3)`|`0.5`|Let's look at the last column only</br>because the first 3 columns have weights = 0.</br> $(0*2 + 1*2 +2*2)/12 = 0.5$|  


```{admonition} Tips
:class: hint
* It helps if you know about: `shape`, `broadcasting` and "vector" math.  
* Consider how `numpy` uses "broadcasting" to adjust the shapes.  
* Leverage `numpy` methods and functionality.  
📝 **Extra Challenge**: Can you write this method in 1 line of code?  
```

