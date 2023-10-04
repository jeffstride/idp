# Writing Effective Comments

Comments in Java are essential for making your code understandable to both yourself and others. They serve as documentation and explanations for the code you've written. However, writing good comments requires balance. In this lesson you’ll learn the clear and concise way of writing comments, with examples of too little, just right, and too many comments.

## Doc-String Comments
Doc-strings are multi-line strings enclosed in triple-quotes (either single or double). They are used to document classes and functions. Here is what makes a strong Doc-String comment:
1. State WHAT the function does. NOT how. And NOT why.
2. Mention by name all the arguments. Types can be inferred (or it is explicitly stated) for each argument.
3. Describe all the return values and special cases.

Doc-strings should not be used anywhere else except as the method descriptor.
Note that they always belong `under` the prototype, not above the prototype (as they are in Java).

## Inline Comments 
Inline comments are single-line comments that appear within the code, providing clarifications or explanations for specific lines or blocks of code. Inline should explain `WHY, HOW, WHAT.` Here is what makes a strong inline comment:
1. All comments should add real value while letting the code speak for itself. Avoid trivial comment such as: this adds one to x
2. The BEST comments state WHY things are happening, such as: we subtract one because we must exclude the last value that is unused in this case
3. Short, tight and efficient code can sometimes be very hard to read. This is when a WHAT comment is vital to have.

When the “what” is obvious, a “how” may not be necessary in the final submission. “How” comments are initially used to help the developer decompose the problem when writing a solution. Developers often write out a few comments that state the steps to take to solve a problem. These can remain as explanations of WHAT if they still add value after the code is complete. 

But, avoid comments like: “loop through each element in the list” if the code is easy to read. However, if the code is sufficiently complicated, “how” comments can truly add value.

It should be clear where vertical spacing belongs, `above` the inline comment (except if it is the first line in the method).

## Too Little
````{tab-set} 
```{tab-item} No Comments
In this example, there are no comments at all. While the code may be simple to understand, it lacks context and explanations. It may be difficult for someone else (or even yourself in the future) to understand the purpose and behavior of these methods.
```python 
def calculate_total(list):
    total = 0
    for element in list:
        total += element
    return total
```
```{tab-item} Doc-String Comments
The example inlcudes a comment, but it does not provide the paramter types or the return type. The explaination is also ambiguous. Does the function take into consideration capital letters? What is the return type? What are the exceptions?
```python
def count_letters(string):
    ''' 
    Takes a string and returns the occurrences of each character
    '''
    dict = {}
    for c in string:
        if(dict.get(c) == None):
            dict[c] = 1
        else:
            dict[c] += 1

    return dict

def main():
  print(count_letters("How much wood could a wood chuck chuck?"))

```
```{tab-item} Inline Comments
This example includes minimal comments, which do not provide meaningful information. While the comment mentions "checks if c exists" it doesn't say where it is checking. It also doesn't clarify that main uses a test to check fro count_letters()
```python
def count_letters(string):
    dict = {}
    for c in string:
        # checks if c exists
        if(dict.get(c) == None):
            dict[c] = 1
        else:
            dict[c] += 1

    return dict

def main():
    # calls count_letters()
    print(count_letters("How much wood could a wood chuck chuck?"))
```
````

## Goldilocks
````{tab-set} 
```{tab-item} Doc-String Comments
This example includes comments at the function level. The comments explain what the function does, what arguments it expects, and what it returns. This level of commenting provides clear and useful information without being excessive.
```python 
def find_largest(numbers):
    '''
    Find the largest value in numbers, an unsorted list of real values. 
    Return as an integer the largest number found. Return None if the list is empty.
    '''
    return None if len(numbers) else int(max(numbers))
```
```{tab-item} Inline Comments
In this case, comments are provided to the function: stats(). The comments are concise and enhance code readability. They aren't redundant and offer clarifications. 
```python
def stats(tuple_args):
    '''
    This functions takes a tuple as an argument and returns the 
    sum, count, and average of all elements as a tuple... 
    (sum, count, avg)
    '''
    s = sum(tuple_args)
    count = len(tuple_args)

    # return a tuple with the mean
    return(s, count, s/count)
    
def main():
    print(stats((1,2,3)))
```
````

## Too Much
````{tab-set} 
```{tab-item} Doc-String Comments
`Excessive comments in doc-string are not penalized, but they cost a lot of effort.`
This example contains excessive comments that provide redundant information. Comments should not restate the obvious. Over-commenting can clutter the code and make it harder to read.
```python 
'''
This is the main module of the application.
It does a lot of things, like managing user input, performing calculations, and displaying results.
Here, I declare a variable 'x' to hold some data.
'''

class Main:

def add(a, b):
    '''
    This method adds two numbers together.
    It takes two parameters, 'a' and 'b', and returns their sum.
    Args: a (int), the first number to be added and b (int), the second number to be added.
    Returns: int, the sum of 'a' and 'b'.
    '''
    return a + b
```

```{tab-item} Inline Comments
Similarly, in this case, it is not essential to use comments to define variables. The language used is also not clean or professional.
```python
def add_all(numbers):
    # Initialize the total sum to zero
    total = 0

    # Loop through the list of numbers and calculate the total sum
    # This loop iterates over each element in the list 'numbers'
    for num in numbers:

        # Inside the loop, we add the current number to the total sum
        total += num

    # Return the total
    return total 
```
````

