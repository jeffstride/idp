# <i class="fas fa-laptop fa-fw"></i> HW1


Welcome to your first take-home assessment! In every assessment, we will define a set of problems we would like you to solve. Even if the assessment is solving some larger problem, we usually break it up into small sub-problems for you to help manage the work. 

## Overview
```{admonition} Note
:class: margin

You'll want to take shortcuts all year. You'll be better off if you follow this pattern.
```
This course will stress a development process called **Test Driven Development**. This means that you write your tests first!
Of course your tests will fail, especially if you don't have the method prototypes (or stubs) created yet. The order of operations
goes like this.


````{tab-set}
```{tab-item} Step 1
Create the method prototype and doc-string. Do not implement!. Use the
python keyword `pass` as a placeholder for the implementation you will provide in step 3.
```python
def problem_1(s):
    '''
    This method will remove the first letter in the string s
    and replace all other occurance of that letter with a space.
    It will return the new string.
    If the string is empty, it will return an empty string.
    '''
    pass
```

```{tab-item} Step 2
Create the test in the test Python file and verify failure by running the test file.
You may need to update the `.replit` file to run the correct code.
```python
from cse163_utils.py import assert_equals
import hw1

def test_problem_1():
    assert_equals(hw1.problem_1('sletstheresbeslight'), 'let there be light')
    assert_equals(hw1.problem_1('ssss'), '   ')
    assert_equals(hw1.problem_1('', ''))
```

```{tab-item} Step 3
implement the method
```python
def problem_1(s):
    '''
    This method will remove the first letter in the string s
    and replace all other occurance of that letter with a space.
    It will return the new string.
    If the string is empty, it will return an empty string.
    '''
    if len(s) == 0:
        return ''
    return s[1:].replace(s[0:1], ' ')
```
````

**For this assessment, we have already implemented some buggy solutions to these problems.** Your job is to identify and fix the bugs.

## Files
* `hw1.py` is the (potentially buggy) code for the problems described below. hw1.py is not a runnable program, so we don’t use the main-method pattern.
* `hw1_test.py` is the file for you to put your own tests.
* `cse163_utils.py` is a helper file that has code to help you test your code. You do not need to look at or modify this file ever.

```{admonition} warning
:class: important
`replit` needs to be configured to run a file. Unfortunately, the way this works has changed a bit over time as replit
adds more features and advances. As of this writing, replit uses [Nix](https://docs.replit.com/tutorials/python/build-with-nix). 
See [Building on Replit](/module-additions/module1/building-in-replit) for more details.
```

* * * 

Here are the details of the assignment.  

Problems to create.  
Testing to do.  
Rubric information.  

