# Notes on MyST 
This page contains example styles to help authors of this site to style stuff correctly.

## Highlight and Hover
<span title="Extra information on hover!" style="background-color: yellow">Test me by hovering over me.</span>

## Code with Lines and Emphasis
```{code-block} python
:linenos:
:emphasize-lines: 3
def my_method(x):
    print(s)
    return x
```

## Icons
Lot's of icons found in `.\html\_static\vendor\fontawesome\6.1.2\css\all.min.css`   
<i class="fas fa-rocket fa-fw"></i> fa-rocket   
<i class="fas fa-prescription-bottle fa-fw"></i> fa-prescription-bottle   
<i class="fas fa-question fa-fw"></i> fa-question  
<i class="fas fa-file-video fa-fw"></i> fa-file-video  
<i class="fas fa-arrow-right fa-fw"></i> fa-arrow-right  
<i class="fas fa-fingerprint fa-fw"></i> fa-fingerprint    
<i class="fas fa-file-download fa-fw"></i> fa-file-download   
<i class="fas fa-download fa-fw"></i> fa-download   

## Reference Examples
Create some text that needs a footnote like this here.<a href="#footnotes"><sup>[1]</sup></a>   

Create a <a href="#footnotes">reference</a> to somewhere on this page in the same way as using footnotes.  

A reference to another page is done similarly. Go to <a href="../Replit/flake8.html#tox.ini"> Flake8 Tox.ini</a>.

## Admonitions
Here are examples of popular admonitions:  
```{admonition} Reference
:class: dropdown seealso
Content is here
```

```{admonition} Note
:class: note
This is a note
```

## Math
`$\sigma = \sqrt{n \cdot p \cdot (1 - p)}$ `  
$\sigma = \sqrt{n \cdot p \cdot (1 - p)}$   

`$\frac{x+y}{a+b}$`  
$\frac{x+y}{a+b}$   

`$f'(x_1) \approx sqrt{2+x_0 \cdot x_1} \pm 1$`  
$f'(x_1) \approx \sqrt{2+x_0 \cdot x_1} \pm 1$     

`$T = \sum_{i=0}^{j} M_i$`
$T = \sum_{i=0}^{j} M_i$


## Tables
### github table
|col1|col2|col3|
|----|----|----|
|value1|a lot of text here that may or may not wrap|more text|
|value2|short|A lot of text here that may or may not wrap. You have no control over the column widths|

### myST
In this table, the structure is much different. There is a title. And, you have some control over the column widths.  
```{list-table} A List Table
:widths: 5 2 30
:header-rows: 1
* - col1
  - col2
  - col3
* - This column is set to width=5
  - Width=2
  - This column has the width set to 30. 
* - Value
  - 20
  - Likely, all the column widths are relative. But, I honestly don't understand the units. And, I'd like to find a way to create a table that doesn't span the entire width, but is more compact.
```

## Footnotes
[1] List all the footnotes here using numbers that match the link in the body. 