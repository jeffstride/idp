# Flake8
This is a command line <a href="https://en.wikipedia.org/wiki/Lint_(software)" target="_blank">lint</a> tool that verifies that your style meets standards.
Many people, including myself, detest the pedantic verification of spaces and line lengths.
However, the tool will help assure that your code looks correct. Once you get
comfortable writing code to the standards, it'll go quickly and naturally. And, your code will be nicely readable!  

```{admonition} Important!
:class: important
Do not install flake8 using the Packages functionality/tab in Replit. In order to have the proper versioning, we need to
install flake8 version 5.0.4 (whereas the default version is 6.0.0). If the flake8 is not installed already, you can
install the correct version by going to the `shell` tab and typing in: `poetry add 'flake8 5.0.4'`. Don't forget the quotes.
```

|Codes|Descriptions|
|-----|------------|
|W291|Trailing whitespace: a line has a space at the end. Although this does assure that a coding file is super clean and professional, it is way more annoying than useful. This error is ignored|
|W504| This warning code indicates a line break after a binary operator. It reminds you that there should not be a line break between a binary operator (e.g., +, -, *, /) and its second operand.|
|W391| This warning code indicates a blank line at the end of a file. It reminds you to remove any unnecessary blank lines after the last line of code in a Python file.|
|W291| This warning code indicates trailing whitespace at the end of a line. It reminds you to remove any spaces or tabs at the end of lines, which can be considered a style violation.|
|W292| This warning code indicates that there are no newline (blank) lines at the end of the file. It is a style reminder that you should include a newline character at the end of the file.|
|E121| This error code indicates an indentation error. It is raised when there are inconsistencies in the indentation of code blocks, such as mismatched or inconsistent indentation levels.|
|E402| This error code indicates a module-level import not at the top of the file. It reminds you that all imports should be placed at the beginning of the file before any other statements or code.|
|E501| This error code indicates that a line of code exceeds the maximum line length allowed. By default, flake8 enforces a maximum line length of 79 characters.|

## tox.ini
```{admonition} Important!
:class: important
Do NOT modify `tox.ini` yourself. Mr. Stride's unit tests will not accept any changes you make to this file.
If you fail flake8, then you'll be penalized.  
```

## E501 line too long
The spirit of the rule is fabulous: your code needs to be readable and lines that are too long detract from readability.
Furthermore, `replit` has a nifty, built-in funtion to help correct these errors: simply type `ctrl+s`. 
**However**, the default 80-character line length (although not completely arbitrary) is too short for modern development
and it doesn't allow for other good conventions such as:  
* descriptive identifier names that are longer  
* concise, inline development style   
* perserving vertical real estate   

We will be customizing the maximum line length to be 110 and this length will be strictly enforced. This is done by adding the
the following configuration to `tox.ini`:  
```python
max-line-length = 110
```

```{admonition} Why 80?
:class: note
There are two good reasons why 80 was the chosen default length.  
1) When you print code out onto paper, the typical horizontal length of a sheet of paper would allow for 80 characters to be printed. Back in the old days, computer programmers would print code out onto paper for review.  
2) Monitors were lower resolution and typically would not allow more than 80 characters to be displayed horizontally across the screen.  

```{admonition} Old Days of Printing
:class: seealso dropdown
Back in the old days, many printers were called <a href="https://en.wikipedia.org/wiki/Dot_matrix" target="_blank">dot matrix</a> printers where each character was comprised of an 6x7 matrix of visible dots.
The paper was <a href="https://en.wikipedia.org/wiki/Continuous_stationery" target="_blank">continuous stationary</a> : each page was linked to the prior page via perforation and had holes on the sides to allow the printer to feed the paper through.
```

Egregiously long lines need to be fixed!