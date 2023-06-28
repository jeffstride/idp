# Printing and Arguments

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
