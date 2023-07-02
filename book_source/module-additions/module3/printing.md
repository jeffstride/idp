# Arguments

I have found it frustrating to visit online API sites to discover their form of 
documentation consists of something like the following:
    `my_method(*args, **kwargs)`  
Especially when there is no mention of what `args` or `kwargs` can be. We can't solve
that, but we can at least understand what `*args, **kwargs` means and how to use them.
The above effectively means the method takes any number of `positional arguments` and
any number of `named arguments`. Let's first define a couple of terms.  
```{card} Important Terms

|Term|Definition|  
|----|----------|  
|_Positional Argument_|Required method arguments that must appear in a specific order|  
|_Named Argument_|Optional method arguments that are given a default value in the prototype (method declaration). They will appear as `name=value`. They can appear in any order after all the positional arguments are provided.|
```

```python
# Example prototype with 4 positional arguments and 3 named arguments
def example_a(value1, value2, value3, value4, named1=1, named2=2, named3=3):
    '''
    value1, value2, value3 & value4 must be present when calling method()
    named1, named2 & named3 are optional because they have default values.
    '''
    print(value1, value2, value3, value4, named1, named2, named3)

# we can call example_a in the following ways
example_a(3, 1, 4, 1)                               # output: 3 1 4 1 1 2 3
example_a('a', 'b', 'c', 'd', named2='foo')         # output: a b c d 1 foo 3
example_a(0, 0, 'a', 'b', named3='bar', named1='foo')#output: 0 0 a b foo 2 bar

# example prototype with 1 required positional argument, any number of
# optional positional arguments, and two optional named arguments
def example_b(value1, *args, named1=1, named2=2):
    '''
    value1 is a required, positional argument
    args is basically a Tuple that represents any number of un-named argments that appear
        before all named arguments
    named1 & named2 are optional, named arguments that are given default values
    '''
    # when we put the '*' in front of args, we unpack the set of
    print(value1 + 10, *args, named1, named2)

# we can call example_b in the following ways:
example_b(5, 10, 15, 20)        # output: 15 10 15 20 1 2
example_b(0, named2='override') # output: 10 1 override

def example_c(value1, *args, named1=1, named2=2, **kwargs):
    '''
    value1 is a required, positional argument
    args is basically a Tuple that represents any number of un-named argments that appear
        before all named arguments
    named1 & named2 are optional, named arguments that are given default values
    kwargs is basically a dictionary that represents any number of named argument
        that appear after all the positional arguments
    '''
    # unpack args to all positional arguments
    # unpack **kwargs to be all named arguments
    print(value1 + 20, named1, named2, *args, **kwargs)
    
example_c(0, named1=10)     # output: 20 10 2
example_c(2, 'foo', named2=0, sep='-') # output: 22-1-0-foo

```

Explain after each example how the output happens. Explain `sep`. Explain why `foo` appears at the end.



# Printing, Arguments & Formatted Strings

Cover the different ways we print and how to format our strings.
We need to understand named arguments, packing and unpacking.
explain `print(*args, **kwargs)`  
explain how kwargs is a dictionary of key/value pairs.  
explain how *args is a list or sequence of values.  
explain named arguments 'end' and 'sep'.

Reference: https://realpython.com/python-f-strings/  
https://docs.python.org/3/library/string.html#format-string-syntax

## %-formatting (old)
print("Hello, %s. You are %s." % (name, adjective))

## formatted printing
```python
float = 2.154327
format_float = "{:.2f}".format(float)
print(format_float)

print("text {0}".format('value'))
```

## f-string

Python's string <a href="https://docs.python.org/3/library/string.html#format-string-syntax" 
target="_blank">formatting</a> functionality as built into Pythons <a href="https://realpython.com/python-f-strings/" 
target="_blank">f-string</a>. The API is a bit complicated to understand. It is similar
to the way Java implements `printf`, only it has different escape sequences and specifics. In short, when a
string literal is preceded with 'f' then the string is expecting to have some
formatting sequence in it. A formatting sequence is embedded inside curly braces `{}` and the text
inside the curly braces is interpreted. It would contain identifiers, method calls, and possibly
formatting options following a colon. Here is the syantax for printing a floating point number with some text label:  

    f'text{<identifer>:.<integer>f}'
    
For example, let's say we do the following:  

    gpa = 3.899
    print(f'GPA={gpa:.2f}')

That code results in printing, `GPA=3.90` (due to rounding to 2 decimal places).
