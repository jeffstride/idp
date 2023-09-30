# Writing Effective Comments

Comments in Java are essential for making your code understandable to both yourself and others. They serve as documentation and explanations for the code you've written. However, writing good comments requires balance. In this lesson you’ll learn the clear and concise way of writing comments, with examples of too little, just right, and too many comments.

There are two goals you want to reach when adding comments. The prototype should explain `WHAT` the code does. The inline should explain `WHY` it does it.

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
```{tab-item} Minimal Comments
This example includes minimal comments, which do not provide meaningful information. While the comment mentions "Process data here," it doesn't explain how it is processed or provide any details about the logic involved.
```python
def process_data(data):
    # Process data here
    pass
```
```{tab-item} Missing Paramater and Return Types
The example inlcudes a comment, but it does not provide the paramter types or the return type. The explaination is also ambiguous. Does the function swap the characters with eachother? With another character? Does the function return anything?
```python
'''

Takes two characters and swaps them in a given word. 

'''
def swap(c1, c2, word):
    # Function body here
    pass
```
````

## Goldilocks
````{tab-set} 
```{tab-item} Function Comments
This example includes comments at the function level. The comments explain what the function does, what arguments it expects, and what it returns. This level of commenting provides clear and useful information without being excessive.
```python 
"""

Find and return the largest number in the given list of numbers.
Args: numbers (list), a list of numbers to search through.
Returns: int, the largest number found in the list.

"""
def find_largest(numbers):
    # Implementation details
    pass
```
```{tab-item} Class Comments
In this case, high-level comments are provided at the class level. These comments give an overview of the class's purpose and the kind of information it stores. It sets the context for the entire class, making it easier to understand its role in the program.
```python
"""

The Student class represents a student in North Creek High School.
It stores basic information about the student, such as name and ID.

"""
class Student:
    # Fields, constructors, and functions go here
```
````

## Too Much
````{tab-set} 
```{tab-item} Excessive Function Comments
This example contains excessive comments that provide redundant information. Comments should not restate the obvious. Over-commenting can clutter the code and make it harder to read.
```python 
"""

This method adds two numbers together.
It takes two parameters, 'a' and 'b', and returns their sum.
Args: a (int), the first number to be added and b (int), the second number to be added.
Returns: int, the sum of 'a' and 'b'.

"""
def add(self, a, b):
    # Addition logic
    pass
```
```{tab-item} Exsessive Class Comments
Similarly, in this case, it is not essential to use comments to define variables. The language used is also not clean or professional.
```python
"""

This is the main module of our application.
It does a lot of things, like managing user input, performing calculations, and displaying results.
Here, we declare a variable 'x' to hold some data.

"""
# Variable declaration
x = 0

class Main:
```
````

