# <i class="fas fa-laptop fa-fw"></i> HW1 - Startup


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
    '''
    Tests the method problem_1()
    '''
    # Tests provided in the handout
    assert_equals(hw1.problem_1('sletstheresbeslight'), 'let there be light')
    assert_equals(hw1.problem_1('ssss'), '   ')
    # Edge Case
    assert_equals(hw1.problem_1('', ''))
    # My extra tests
    assert_equals(hw1.problem_1('?My?Tests?are?better!', 'My Tests are better!'))
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

## Files and Tests
````{tab-set}
```{tab-item} Provided Files
You are provided with the following files:  
* `hw1.py` is the (potentially buggy) code for the problems described below. hw1.py is not a runnable program, so we don’t use the main-method pattern.
* `hw1_test.py` is the file for you to put your own tests.
* `cse163_utils.py` is a helper file that has code to help you test your code. You do not need to look at or modify this file ever.  
* `tox.ini` is a `flake8` configuration file that allows us to customize the types of warnings and errors students must fix.   
```
```{tab-item} Files to Submit
You must submit your work to the <a href="https://autograder-nchs.vercel.app/login" target="_blank">Code Submission Site</a>.  

**Submit only**:  
* `hw1.py`  
* `hw1_test.py` : must have `main-pattern` to run all test methods 
```
```{tab-item} Replit Unit Tests
The only Unit Test provided in Replit is for the _Challenge Question_ which is not graded.
```
````
```{admonition} Run in Replit
:class: note
For this assignment `replit` has been to be configured to run `hw1_test.py`.
See [Building in Replit](/Topics/Replit/building-in-replit) for how this is done. In future assignments,
you may want to modify this as you develop.  
```

* * * 
## Implementation
In the file named `hw1.py`, implement three methods: `funky_sum`, `total`, `swip_swap`. The description for each
method is found in the tabs below.
> Note that there is a challenge question which is optional and not graded. See the <a href="#challenge-question">Challenge Question</a> section down below for details.

````{tab-set}
```{tab-item} funky_sum
<i class="fas fa-pen-square fa-fw"></i> **Write** a function `funky_sum` that does a special sum to combine two numbers. An initial (but incomplete) implementation has already been done for you! We will revisit funky_sum later in the spec to fix a bug in this initial code.

The function should take three parameters, the first two are numbers, `a` and `b`, to combine and a third, `mix`, is a number to determine the ratio to use from each. `mix` acts as a "slider" to control how much to use of each number. If mix is 0 or less, the result should be the same as `a`. On the other hand, if `mix` is 1 or more, the result should be the same as `b`. For any value of `mix` between 0 and 1, it should add `1-mix` times `a` and `mix` times `b`. The technical name for this operation is "linear interpolation".  

Here are some examples that you should make sure appear in `hw1_test.py`:
| call | returns |
|------|---------|
|funky_sum(1, 3, 0.5)| 2.0| 
|funky_sum(1, 3, 0)|1| 
|funky_sum(1, 3, 0.25)| 1.5| 
|funky_sum(1, 3, 0.6) |2.2|
|funky_sum(1, 3, 1)|3|
```

```{tab-item} total
<i class="fas fa-pen-square fa-fw"></i> **Write** a function total that takes a number `n` and returns the sum of the integers from 0 (inclusive) to n (inclusive). If `n` is negative, the function should return the value `None` instead.  

This method already been written for you, so you will not need to modify any code for this function. **But**, you will have to add **doc-string documentation** and add **more tests** to assure all special cases are covered.

```

```{tab-item} swip_swap
<i class="fas fa-pen-square fa-fw"></i> **Write** a function `swip_swap` that takes a string source and characters `c1` and `c2` and returns a copy of source with all occurrences of c1 and c2 swapped. You may assume that the c1 and c2 are single characters. Use str concatenation with the + operator to solve this problem.

Here are some examples that you should make sure appear in `hw1_test.py`:
| call | returns | 
|------|---------| 
|swip_swap('foobar', 'f', 'o')| 'offbar'| 
|swip_swap('foobar', 'b', 'c')| 'foocar'| 
|swip_swap('foobar', 'z', 'c')| 'foobar'| 

```{admonition} important
In order to demonstrate the learning objectives for this problem, you should **NOT** use the string `replace` function or use any data structures like `list` to solve this problem.
```

````

## Testing
<i class="fas fa-pen-square fa-fw"></i> **Test** the three functions in with test method in `hw1_test.py`. The original code in `hw1.py` remains unchanged. Each testing method should include the tests provided in this document along with **at least 2 more** tests that you make up. All of these methods make calls to `assert_equals`. 

Make sure each test function is actually called in `main` and that you use the _main-pattern_ as shown here!

```python
def main():
    test_swip_swap()
    test_total()
    test_funky_sum()


if __name__ == '__main__':
    main()
```

## Documentation
<i class="fas fa-pen-square fa-fw"></i> **Document** the code in `hw1.py` and `hw1_test.py`.

There is no documentation in the provided code! We recommend writing your documentation FIRST (in Step 1). Writing documentation for your function is a great way to start to get you thinking about what your method needs to do. You should go through and add the following documentation:

* Each function in `hw1.py` and `hw1_test.py` should have a doc-string comment describing their parameters, returns and behavior.

* Each file `hw1.py` and `hw1_test.py` should have a doc-string comment as the first lines of that file. This comment should describe what the whole file is for. A doc-string for a file looks the same as a doc-string for a function, but goes as the first lines of the file. Each doc-string for the file should have your name and your section in it as well. Since this assignment doesn’t really have a context, the description for hw1.py can just say something like "Implements the functions for HW1".

Importantly, it helps to think about who the audience of your comments will be. They are interested in knowing:  
1. **WHAT** your function does
2. **RETURN** values of the function, including special cases. 

The audience of your comments are **NOT** looking for you to simply rewrite the code in English. They do **NOT** want to know how the method works. Those types of comments belong in the code as `# inline comments`. You commonly want to avoid phrases that are telling the reader how you accomplish something (e.g. “uses a for loop”) since that is a little too detailed into the specific implementation. Instead, describe your function at a high-level; mimic documentation that you find online about a method. 

For example, when you read the <a href="https://docs.python.org/3/library/stdtypes.html#str.split" target="_blank">documentation</a> on the `split` method, notice that it doesn't tell you anything about the code. It tells you what it does!  

```{admonition} hint
Make sure to describe any import edge-cases that the reader might want to know about. For example, does your function ever return `None`?
```

Test method doc-strings do not need to be elaborate. While they are still required, they can be very simple such as: 
```{admonition} Sample Test Comment
:class: dropdown

```python
def test_method_x():
    '''
    Test the method_x().
    '''
``` 

## Challenge Question

**OPTIONAL**: This programming method is not graded and is here for those students who already know Python and want to flex some of their intellectual muscle.  
> **NOTE**: If you implement this method, you'll need to document all methods fully with doc-strings so that all the grading scripts pass. You don't want to have your grade drop!  

```{admonition} important
This Challenge Question is OPTIONAL!! It is NOT graded.
```
**Task**: <i class="fas fa-pen-square fa-fw"></i> Implement a method named `simple_decode` that is a simple decoding of a message that has no more than 16 unique characters in it. This method takes two arguments:  
* `key` - a list of letters (no more than 16 long)
* `encoded` - a list of bytes where each nibble (4-bits) of each byte is the index of letter as found in key  

This method will return the decoded message as a string. 

For example:
```python
    simple_decode(['l', 'e', 'h', 'o'], [33, 0, 48, 1]) # returns 'hello'
```
In summary, the list of integers decodes as follows:
```
    33 = 'he'
    0 = 'll'
    48 = 'o'
    1 = odd length encryption. Ignore last nibble.
```

In more detail:  
```
    The first integer 33 in binary is 0010 0001.  
        0010 is binary for 2 and 'h' is at index 2.  
        0001 is binary for 1 and 'e' is at index 1.  
    And, the second integer value is 0, or 0000 0000.  
        This represents two characters, each at index 0. 'll'  
    48 in binary is 0011 0000  
        0011 is binary for 3 and 'o' is at index 3.  
    The very last nibble is ignored because the last integer value is 1  
    which means that the message is odd-lengthed.  
    If the last integer value was 0, then we would include the letter at index 0.
```

Rubric information can be found in the instruction in the Replit project.  

