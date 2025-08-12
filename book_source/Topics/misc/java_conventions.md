
<style>
div.good-code div pre {
    background-color: rgba(209, 255, 211, 0.5) !important; /* Light green */
}
div.bad-code div pre {
    background-color: rgba(255, 209, 209, 0.5) !important;
}
div.okay-code div pre {
    background-color: rgba(253, 255, 201, 0.5) !important;
}
</style>
# CSS 142/143 Code Quality Guide

## Overview

Writing Java code isn't just about writing code that compiles and
works. If we wanted code that just got a computer to follow our
directions, why not just write it in binary? Truth is, code isn't
written for computers; it's written for people. Programming in the real
world is a highly collaborative activity, so it's very important to be
able to write code that is easy to work with and understand. Having
clean, readable code also makes finding bugs and errors in your code
significantly easier. This code quality guide contains a set of
guidelines we expect you to follow when writing code. This document
covers the entire quarter, so it is not meant to be something that you
memorize and understand entirely through one read through. Rather, it is
a reference guide that you should be able to use to look up rules and
examples.

<a id="java-conventions"></a>
## Java Conventions

Java syntax is writing code in a way that allows it to compile.
Conventions are things that don't affect whether the code will compile,
but are just generally accepted as part of writing good Java code, and
are things that you should adhere to ensure you are writing good,
readable code.

### Curly Braces 

In Java curly braces are used to compartmentalize blocks of code. Lots
of languages use curly braces, and Java has its a convention for how to
use them. An opening curly brace should be placed at the end of the line
that opened it, and the closing curly brace should be on a line by
itself at the same level of indentation as the line with the opening
curly brace.


```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```


### Indentation

Indentation is an important way to help distinguish blocks of code. You
should indent your program one tab further every time you open a curly
brace `{` and indent one tab less every time you close a curly brace
`}`.

> A tab should generally be 3 or 4 spaces, and you can set the size of
> your tab in your compiler. The jGrasp default is 3 spaces

Take these two examples:

```{code-block} java
:class: bad-code
public static void main(String[] args) {
for (int i = 0; i < 10; i++) {
if (i % 2 == 0) {
System.out.println("Hello world!");
}
}
}
```

This method has no indentation, and is super hard to read as a result.
Now look at the second method below:

```{code-block} java
:class: good-code
public static void main(String[] args) {
    for (int i = 0; i < 10; i++) {
        if (i % 2 == 0) {
            System.out.println("Hello world");
        }
    }
}
```

Indentation makes code easier to read. It helps the reader see what code
is nested where, and where structures like `if` statements and loops
start and end.

> You can actually have jGRASP fix all your indentation for you! To the
> right of the **Undo** button is the **Generate CSD** button, which
> will automatically indent your code and add some structural
> annotations on your code, which can be removed with the next button to
> the right, the **Remove CSD** button.

### Long Lines and Wrapping

To keep our code nice and compact and improve readability, lines of code
should ideally max out at ~80 characters, and should **never** exceed 100
characters in length. Lines that are too long should be broken up and
wrapped to the next line.

> Note that in jGrasp, you can check your line length by putting your
> cursor at the end of the line and check the bottom right corner. There
> should be something that says "Col:"" and then the number of
> characters in the line.

To break up a long comment, you can simply split the comment into two or
more lines:

```java
// THIS IS A BAD COMMENT
// this is a bad comment because it is just so gosh darn long (perhaps not that long, but long enough) that it just makes it so hard to read

// THIS IS A GOOD COMMENT
// this is a good comment because when it reaches the point where it is too long,
// the comment just moves to the next line
```

Breaking up lines of code is a little more complicated. Choosing where
to break up your lines can be a little arbitrary, but it's usually best
to break the line *after* things like commas and operators. IMPORTANT:
You cannot break a String up between lines. If you want to break a
String up, you need to use two separate Strings that are concatenated.
There are two conventions for wrapping a line of code:

1.  You can leave a hanging indent of two tabs relative to the start of
    the first line, like so:

```java
// Because the String to be printed is so long, it gets wrapped to the next line
public static void printReallyLongLine() {
    System.out.println("wow this line is so long it's like unreasonably long like" +
            "honestly it's so long why even");
}
```

2.  Or, if the long line has something in parentheses, like a method
    header, you can align the code inside the parentheses, like so:

```java
public static void thisMethodHeaderIsReallyLong(int thing, int otherThing,
                                                int moreThings, int anotherThing)
```

> Note that these are very bad method and variable names, and you should
> not use these as an example. These are just examples of long lines.

### Spacing

It might seem trivial, but spacing is very important for writing
readable code. Here are some examples of Java conventions for good
spacing for your code:

|Code|	Good Spacing|	Bad Spacing|
|----|--------------|--------------|
|Class Header|`public class GoodSpacing {`|	`public class BadSpacing{`|
|Method Header|	`public void method(int param, int param2) {`|	`public void method (int param,int param2){`|
|Method Call|	`method(7, 2);`	|`method(7,2);`|
|for loop|	`for (int i = 0; i < 5; i++) {`|	`for(int i=0;i<5;i++){`|
|while loop|	`while (test) {`|	`while(test){`|
|Array Initialization|	`int[] arr = new int[5];`|	`int [] arr=new int [5];`|
|Variable Initialization|	`int x = -5 * j + y % 2;`|	`int x=-5*j+y%2;`

> Note the spacing in expressions. Generally, you should always leave a
> space on either side of an operator (+, -, =, etc.). The only
> exceptions are `++`, `--`, and using `-` to express negative numbers
> (i.e. `-5`).

### Spacing Between Methods 

Similar to spacing within lines of code, we want to ensure that we have
spacing in the structure of our code to keep our code looking readable.
You should always include a blank line between methods to make sure your
code is easy to read through.


```{code-block} java
:class: good-code
// Good Example
public class GoodSpacing {
    public static void main(String[] args) {
        ...
    }

    public static void method() {
        ...
    }

    public static void anotherMethod() {
        ...
    }
}
```

## Names

### Naming Conventions 

We have certain conventions for how we name things in Java. Here are the
conventions we use for different kinds of names in Java:

- **Method & Variable Names**: These should be **camelCased**, a
  convention where the first letter of every word after the first is
  uppercased.
- **Class Names**: These should be **PascalCased**, a subset of camel
  casing where the first letter of the first word is also uppercased.
- **Constant Names**: These should be **SCREAMING_CASED**, in all
  uppercase with words separated by underscores.

### Methods are Verbs

Methods do things. They should only do **one** thing. Your method names
should be *VERBS* that describe the one thing that the method does.  

```{code-block} java
:class: good-code
public int incrementX(int delta) {
    this.x += delta;
}
```
### Descriptive Names

The name of a variable should describe the value it stores and what it
represents. Similarly, the name of a method should describe the task of
the method. As a general rule of thumb, class and variable names should
be nouns, and method names should be verbs. Abbreviations should not be
used unless they are generally accepted abbreviations or very obvious,
like num for number. It's usually best to avoid abbreviations. 

```{admonition} Single-Letter Identifiers
:class: important
**Avoid** variable names that are just a single letter. 
```

Students should leverage **Semantic Naming** when picking variable names (i.e. identifiers.)  

```{admonition} Definition
:class: tip
**Semantic naming** means choosing identifiers that clearly and accurately describe the purpose, role, or content of the item they represent in the code.
```

### NO Single-Letter Identifiers
It is common to use `i` and `j` for loop variable names because 
developers are basically lazy. There is a [good amount of history](https://stackoverflow.com/questions/4137785/why-are-variables-i-and-j-used-for-counters) in this usage. However, it can lead to confusion when
other identifiers are better. While it is convenient, common and alluring to use `i` for outer-loops,
and `j`for once-nested loops, it is often better to use a name that adds clarity. For example, if we
are iterating through a matrix, the identifiers `row` and `col` offer a great semantic fit and can
improve readability and reduce bugs. 

```{code-block} java
:class: good-code
int[][] matrix = new int[10][12];
for (int row = 0; row < matrix.length; row++) {
    for (int col = 0; col < matrix[row].length; col++) {
        System.out.printf("matrix[%d][%d] = %d\n", row, col, matrix[row][col]);
    }
}
```

When iterating through a single dimension array, it is acceptable to use `i`. However, a nicer approach is to use `index`.

```{code-block} java
:class: okay-code
int[] arr = new int[20];

// Acceptable
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```
```{code-block} java
:class: good-code
int[] arr = new int[20];

// Better
for (int index = 0; index < arr.length; index++) {
    System.out.println(arr[index]);
}
```

```{admonition} Note
:class: note
Be careful of copy-paste errors! Using `i` and `j` can lead to bugs.
```{code-block} java
:class: bad-code
// i looks an aweful lot like j
for (int i = 1; i < 10; i++) {
    for (int j = 0; j < i; i++) {
        System.out.println("This loop never ends!")
    }
}
```
#### Exceptions

Here are a few tabs to click on that allow you to explore the very few exceptions to using single-letter identifiers.
````{tab-set} 
```{tab-item} Graphics and Random
It is okay to use single-letter identifiers for the `Graphics` and `Random` objects because that is a common Java convention.
```{code-block} java
:class: okay-code
public void draw(Graphics g) {
    Random r = new Random();
}
```
```{tab-item} Coordinates
`(x, y)` are what we actually call
Cartesian coordinates, so they're actually great variable names for
this purpose (but, again, only for coordinates). Similarly, `r` is a
good variable name for describing Polar coordinates (unfortunately
there's no theta key, but if you can get the character it's also
acceptable for a polar coordinate (a little more work than it's
probably worth)).
```{code-block} java
:class: okay-code
public double getDistance(int x, int y) {
    return Math.sqrt(x * x + y * y);
}
```
```{tab-item} Non-Semantic Loops
There are times when we simply need to iterate and there is nothing semantic about the loop at all. In these cases, using `i` is good.
```{code-block} java
:class: good-code
// Nothing semantic to attach to 'i'
for (int i = 0; i < 10; i++) {
    System.out.print("*");
}
```
````
## Methods 
Technically, you could write an entire program in that program's main
method. However, this would be an incredibly bad idea. Your main method
could end up being thousands of lines long. It's generally considered
good practice to factor your code into methods. Here are a few reasons
why:

1.  **Methods Reduce Redundancy:** Often, you will want the exact same
    or very similar tasks multiple times in your program. Rather than
    writing the same code multiple times, which would be redundant, you
    can factor that code into a method that can be called throughout
    your program to perform that task. We can even use parameters and
    returns to create methods that have even more functionality to
    further reduce redundancy. Remember, you should *never* be copying
    and pasting code.
2.  **Methods Represent Tasks:** Even if code isn't redundant, it can
    still be a good idea to factor it into a method. Methods should
    represent a concrete task. A good example is printing an intro to
    your program; it's something you'll only do once, but it's a
    distinct task, so it makes sense to factor it into a method. An
    important aspect of this is making main a concise summary of the
    program. main runs the program, but it shouldn't be cluttered with
    all of the sub-tasks required to do that. Those tasks should each be
    factored into their own methods, whether or not they're redundant.
    Factoring code into methods with distinct tasks also makes it easier
    to reuse your code. If there's a method where you perform 2 tasks,
    and then later only want to perform only one, you couldn't call
    your existing method because you don't want to perform both tasks.
    It would be better to structure each task into its own method to
    make it more reusable.

A few things to avoid:

- **Trivial methods** do so little that their existence is pointless.
  Methods with just one print statement or one method call are good
  examples. One-line methods can be non-trivial if you are factoring a
  common calculation into a method, for instance, but with methods with
  so little code, you should generally consider whether or not the
  method is improving your program.
- Avoid cases where you have **unnecessary parameters and returns**.
  Methods only need to return a value if you plan on catching and using
  that value when you call your method. Otherwise, your method should
  just have a void return type. Similarly, you should only pass in
  parameters that you need. Parameters that you never use in your method
  or whose value could be calculated from other parameters are
  unnecessary. If you pass a parameter into your method but never use
  the value passed in (i.e. you immediately set its value to something
  else), you might want to consider whether you need that parameter at
  all, or if that value could be a local variable.  
- Avoid introducing `state` variables when method arguments and return values 
  provide context. For example, if we want to generate an ASCII Art `String`,
  we should probably pass in the row value and return a `String`.  (See code below.)

```{code-block} java
:class: bad-code
// Very Bad Example that introduces state
public class AsciiArt {
    private String line;
    private int lineNumber;

    public void drawArt() {
        for (int i = 0; i < 10; i++) {
            this.lineNumber = i;
            createLine();
            System.out.println(this.line);
        }
    }
    public void createLine() { 
        // ...
    }
}
```
```{code-block} java
:class: good-code
// Much Better: Using arguments and return values
public class AsciiArt {
    private String line;
    private int lineNumber;

    public void drawArt() {
        for (int lineNum = 0; lineNum < 10; lineNum++) {
            String line = createLine(lineNum);
            System.out.println(line);
        }
    }
    public String createLine(int lineNum) { 
        // ...
    }
}
```
## Printing

There are a few basic rules you should follow for printing in Java:

- You should always print a blank line using `System.out.println()`. Printing an empty String (`System.out.println("")`) is considered bad style; it makes the intention less clear.  
- `\n` should never be used in `print` and `println` statements.  
- Rather than have a bunch of adjacent print statements, you should combine them into one where you can. `System.out.println("**")` is much preferred to `System.out.print("**"); System.out.println();`  

## Variables

Variables are used to store values so that we can access the same values
in multiple places without having to do the same computations to get
that value every time. However, there are some important things to
consider when using variables:

### Scoping 

You should declare your variables in the smallest scope necessary. If a
variable only needs to keep its value through one iteration of a loop,
you should declare it in the loop. If a variable needs to keep track of
something across multiple iterations of a loop, you should declare it
outside the loop. If you have a variable that you need to use in
multiple places throughout your program, it's generally a good idea to
declare it in main and pass it where it's needed using parameters and
returns.

### Constants 

Some values are used all across your program. This is where it's good
to make a class constant. Constants are unchanging values that exist
everywhere in your program and represent some important value in your
program. For example, the Math class has a constant for the value of PI,
because it's an important value that is used often in the class and
needs to have the same value everywhere. Constants also make code easier
to change. Rather than having to change a value everywhere it is used,
you can just change the value of the constant to change that value
everywhere in the program that the constant is used. Constants should
always be declared as `public static final <CONSTANT_NAME>`.
The `final` keyword means that they cannot be changed after declaration.

## Types 

### Primitives vs Wrapper Classes

Every primitive type has an Object that is called a *wrapper class* that
essentially represents the same value, but as an object, for example:

- `Integer` for `int`  
- `Double` for `double`  
- `Boolean` for `boolean`  

While these do represent the same values and can for all intents and
purposes be used the same, you should always use the primitive type over
the wrapper class whenever possible. There are some cases where you need
to use the wrapper class (making an ArrayList or other data structure to
contain a primitive type), but you should always prefer using the
primitive type when possible.

### int vs double

`int`s and `double`s both represent numbers and technically, anything that
can be represented by an int can also be represented by a double.
However, just because it can doesn't mean it should. You should always
use the type that best represents the value you are storing; a
percentage might make sense as a double, but a count should always be a
whole number and should therefore be an int. Make sure to consider what
your variables are representing before making them all doubles when they
shouldn't be.

### booleans

Similarly, there are a few different ways you can represent a true/false
(or yes/no) value. You could represent it with an int as a 1 or a 0, or
even with a String as "yes" or "no" or "true" or "false",
however, there's a better type to represent that. You're representing
one of two values, and that is exactly what a boolean should be used
for. booleans represent a `true` or `false` value, and should always be used
when you're saving some variable that represents one of two states.

## Loops

Something important to first consider is if you actually need a loop.
Loops should be used to perform repeated actions. If you only want to do
something once, then there's no point in having a loop, since you could
just include the code without the loop and it would do the same thing.

```{code-block} java
:class: bad-code
// Bad Example
public static int square (int num) {
    int square = num;
    for (int i = 0; i < 1; i++) {
        square *= num;
    }
    return square;
}
```

In this case, we're using a loop to perform an action that we only need
to do once. We can replace this entire loop with the code inside it and
that would not change anything about what happens when we run the code.

```{code-block} java
:class: good-code
// Good Example
public static int square (int num) {
    int square = num;
    square *= num;
    return square;
}
```

Similarly, if you only want to do something once after a bunch of
repetitions, you should not include that code in the loop, because it's
not actually repeating. For example:

```{code-block} java
:class: bad-code
// Bad Example
for (int i = 0; i <= 5; i++) {
    System.out.print("*");
    if (i == 5) {
        System.out.println(" done");
    }
}
```

In this code they are only printing "done" at the end of the last
iteration, so they should just pull that out of the loop, like this:

```{code-block} java
:class: good-code
// Good Example
for (int i = 0; i <= 5; i++) {
    System.out.print("*");
}
System.out.println(" done");
```


Always make sure you are using the right kind of loop. `for` loops should be used when you
know how many times you want to perform a repeated action (these are
very helpful for String and array traversals).
`while` and `do-while` loops are great for
when you aren't sure how many times your loop will run.

> The difference between a `while` and `do-while` loop is that a do-while is
> guaranteed to run at least once and then function as a while loop. A
> while loop may never run, but a do-while loop is guaranteed to run at
> least once.

## Conditionals

### if/else Structure Choice

Each set of if/else if/else branches can go into at most 1 branch, and
an else branch guarantees that the program will go into a branch. When
using conditionals in your program, you should use a structure that best
matches the min and max number of branches you want to execute. For
instance, take the following program:

```{code-block} java
:class: bad-code
// Bad Example
int x = r.nextInt(5) - 2; // range from -2 to 2
if (x < 0) {
    System.out.println("positive number generated");
}
if (x > 0) {
    System.out.println("negative generated");
}
if (x == 0) {
    System.out.println("0 generated");
}
```

The program as it is currently structured could go into 0-3 branches.
However, because x can only be one value, the program logically should
only go into 1 branch, so it would be better to use `else if`s,
like so:

```{code-block} java
:class: okay-code
// Okay Example
int x = r.nextInt(4);
if (x < 0) {
    System.out.println("positive number generated");
} else if (x > 0) {
    System.out.println("negative number generated");
} else if (x == 0) {
    System.out.println("0 generated");
}
```

This ensures that the program will go into a maximum of 1 branch.
However, this structure could still go into 0 branches, and the program
should go into exactly 1. There are 3 possibilities and one of them must
be true every time. The best way to structure this program would be to
write a conditional structure that goes into exactly 1 branch:

```{code-block} java
:class: good-code
// Good Example
int x = r.nextInt(4);
if (x > 0) {
    System.out.println("positive number generated");
} else if (x < 0) {
    System.out.println("negative number generated");
} else { // x == 0
    System.out.println("0 generated");
}
```

Note that all three of these programs do the same thing externally.
However, the last program is the best stylistically because the other
structures imply to anyone reading the code that x could fall into none
of the branches, which we know is not possible.

### Useless Branches

You should never write code that does nothing, and conditionals are a
good example of this. Remember, every conditional doesn't need to have
an else if or else branch; you should only write these branches when
they're needed. Take the following code:

```{code-block} java
:class: bad-code
// Bad Example
System.out.print("How many numbers? ");
int nums = console.nextInt();
int max = 0;
for (int i = 0; i < nums; i++) {
    System.out.print("Input a positive integer: ");
    int n =  console.nextInt();
    if (n > max) {
        max = n;
    } else {
        max = max;
    }
}
```

In the else branch above, all that's happening is setting
`max = max`, which does nothing. Since this line of
code does nothing, we can remove it:

```{code-block} java
:class: bad-code
if (n > max) {
    max = n;
} else {
}
```

However, now the else branch is empty, and can be removed completely:

```{code-block} java
:class: good-code
if (n > max) {
    max = n;
}
```

Similarly, sometimes you have nothing in your if branch and only want to
execute code if the condition is false. In that case, you should
structure your code with the opposite condition. Take the conditional
from the previous example. If it had been structured like this:

```{code-block} java
:class: bad-code
if (n <= max) {
} else {
    max = n;
}
```

We again have an empty branch, but can't remove it and have just an
else. Instead, just use an if branch with the opposite condition, which
eliminates the need for the empty branch.

```{code-block} java
:class: good-code
if (n > max) {
    max = n;
}
```
### Factoring

Conditionals are used to separate chunks of code that should be executed
under specific conditions. If code is repeated between all the branches,
then that means that that code should be executed regardless of the
condition. Take the following code:

```{code-block} java
:class: bad-code
int num = console.nextInt();
if (num % 2 == 0) {
    System.out.println("Your number was even.");
    return num;
} else {
    System.out.println("Your number was odd.");
    return num;
}
```

In both branches of the conditional, the return statement is the same.
The only thing that is actually differs based on the condition is the
printed statement, so that is all that should be inside the conditional.
The redundant code should be factored out below the conditional:

```{code-block} java
:class: good-code
int num = console.nextInt();
if (num % 2 == 0) {
    System.out.println("Your number was even.");
} else {
    System.out.println("Your number was odd.");
}
return num;
```

### Boolean Zen
Bbooleans represent a `true` or `false` value, and an equality test also
returns a true or false value, so there's no reason to test if a
boolean is equal to true or false. For instance, instead of:

```{code-block} java
:class: bad-code
if (test == true) {
    // do something
}
```

We can actually just use test directly:

```{code-block} java
:class: good-code
if (test) {
    // do something
}
```

Similarly, if we want to execute code when test is false, then we want
to execute when `!test` is true, so instead of testing:

```{code-block} java
:class: bad-code
if (test == false) {
    // do something
}
```

We should just do the following instead:

```{code-block} java
:class: good-code
if (!test) {
    // do something
}
```

Similarly, we can use boolean zen to concisely return a boolean based on
a test as well. Look at this code:

```{code-block} java
:class: bad-code
if (test) {
    return true;
} else {
    return false;
}
```

This code returns true when test is true, and false when test is false;
it basically just returns the value of test. The entire conditional can
be replaced with one line of code:

```{code-block} java
:class: good-code
return test;
```

We can also use boolean zen to make giving values to boolean variables
more concise. Check out this code:

```{code-block} java
:class: bad-code
int age = console.nextInt();
boolean canDrive;
if (age >= 16) {
    canDrive = true;
} else {
    canDrive = false;
}
```

`age >= 16` returns a boolean value, and if it's true `canDrive` is
set to true, and if it's false `canDrive` is set to
false. This is the same situation as the return, so instead of the
conditional we can just set canDrive directly equal to
`age >= 16`:

```{code-block} java
:class: good-code
// Good Example
int age = console.nextInt();
boolean canDrive = (age >= 16);
```

## Using Objects 

It's generally good to try to minimize the number of objects your
program creates. For example, rather than creating a Scanner that takes
in user input in every method where your program needs to take in user
input, it would be better to create one Scanner that takes in user input
in main and pass that Scanner as a parameter to all of the methods that
need it. The same goes for Random objects, Graphics objects, and any
other objects that do the same thing throughout your program. See the
following two programs for examples:

```{code-block} java
:class: bad-code
// BAD
public static void main(String[] args) {
    Scanner console = new Scanner(System.in);
    ...
    method1();
}

public static void method1() {
    Scanner console = new Scanner(System.in);
    ...
}
```

```{code-block} java
:class: good-code
// GOOD
public static void main(String[] args) {
    Scanner console = new Scanner(System.in);
    ...
    method1(console);
}

public static void method1(Scanner console) {
    ...
}
```

## Arrays 

Arrays can be used to store multiple values, but with great power comes
great responsibility. Arrays should be used to store related values.
They should not be used to store multiple independent values. For
instance:

```{code-block} java
:class: bad-code
int[] numbers = new int[3];
System.out.print("What day of the month is it (1-31)? ");
numbers[0] = console.nextInt();
System.out.print("What is the temperature today? ");
numbers[1] = console.nextInt();
System.out.print("How old are you? ");
numbers[2] = console.nextInt();
```

This is an example of cramming a bunch of data into an array even though
that data has nothing to do with each other.

> On a similar note, sometimes it can make sense to return an array, but
> just because you **can** return an array doesn't mean you should use
> it as a way to hack returning multiple values from a method.

### Unrolling Arrays

Often when using arrays, you need to access data from a certain range of
indices (usually the entire array). To do this, you should always use a
loop to traverse the indices of the array, rather than "unrolling" the
array by manually accessing each index of the array. Even if you know
exactly how many items are in your array, using a loop is better
stylistically. It makes your code much more flexible; you could change
the size of your array without having to change the way you access the
array's elements!

```{code-block} java
:class: bad-code
double[] temperatures = {32,41,39,58};

// BAD APPROACH: unrolling
double avgTemp1 = 0;
avgTemp1 += temperatures[0];
avgTemp1 += temperatures[1];
avgTemp1 += temperatures[2];
avgTemp1 += temperatures[3];
avgTemp1 = avgTemp / temperatures.length;
```

```{code-block} java
:class: bad-code
// Also a bad approach. Even though it's all in one line,
// it's still manually unrolling the array and therefore inflexible
double avgTemp2 = temperatures[0] + temperatures[1] + temperatures[2] + temperatures[3];
avgTemp2 = avgTemp2 / temperatures.length;
```

```{code-block} java
:class: good-code
// GOOD APPROACH: array traversal
double avgTemp = 0;
for (int i = 0; i < numbers.length; i++) {
    avgTemp += temperatures[i];
}
avgTemp = avgTemp / temperatures.length
```

## Creating Objects

### Fields

The current state of your object is stored in its fields. Because of
this, the fields of your objects must **always** be declared private.
This ensures that no client of your object will be able to directly
change the state of your object in a way that you haven't allowed them
to.

### Constructors

A line of code where you are creating a variable, like
`int num = 1`, is
doing 2 things. It declares a variable `num` and then
sets the value of `num` to 1. These two steps are the
variable **declaration** and **initialization**:

```java
int num; // declaration
num = 1; // initialization
```

Normally, we combine these into one line of code, but fields must exist
in the scope of the entire class but must also be initialized in the
constructor. For that reason, we put all the *field declarations* at the
top of the program underneath the class header, and all *field
initializations* should be done in the constructor.

```java
public class SomeClass {
    private int someField;

    public SomeClass() {
        someField = 1;
    }
}
```
## Commenting Your Code
it is difficult for a new programmer to understand what to comment. One pitfall is to over comment the code by adding comments that add no insight and essentially repeat the code. A good convention is to let the code speak for itself.

Commenting code is a skill that improves with experience, and learning to strike the right balance between clarity and conciseness is key. Here's a short lesson tailored for new programmers on **what makes good comments** in code.

### Principles of Good Commenting

1. **Explain the "why", not the "what"**  
   If the code is clear, you don’t need to explain what it does—explain why it’s doing it.

2. **Avoid redundant comments**  
   Comments that simply restate the code are noise and should be avoided.

3. **Use comments to clarify complex logic**  
   If a piece of code involves tricky logic or non-obvious decisions, explain it.

4. **Document assumptions and side effects**  
   If your code relies on certain conditions or affects other parts of the system, note that.

5. **Keep comments up to date**  
   Outdated comments are worse than no comments—they mislead.


Documenting your code is an essential part of computer programming.
Documenting means writing English comments about your code that explain
what it does. It makes your code easier to maintain and update. It also
makes your code easier to understand, both for yourself and for others
working on the same code. This section of the code quality guide will
show you how to write good comments.

There are two ways to write comments in Java; *single-line* and
*multi-line* comments:

```java
// This is a single-line comment
```

```java
/* This is a
multi-line comment */
```

Either way is fine for writing comments, but generally programmers like
to stick with one or the other for consistency.

### Stack the Comments
Your inline comments should be stacked vertically.
```{code-block} java
:class: bad-code
    // Side-Comments get ugly. Avoid them.
    public static int workHard(int grit) {
        int style = grit * grit; // squaring grit is a good style
        int foo = (int) Math.sqrt(style / Math.PI); // comments don't align nicely and they often go long
        if (style == 0) { // check the case where we have no style
            foo = 1; // one is the minimum allowed for foo
        }
    }
```
```{code-block} java
:class: good-code
    // Good Comments are easy to read
    public static int workHard(int grit) {
         // squaring grit is a good style
        int style = grit * grit;

        // stacked comments align nicely and look cleaner
        int foo = (int) Math.sqrt(style / Math.PI);

        // comments above an if describe the predicate (condition).
        // Check if we have no style.
        if (style == 0) {
            // Comments inside the if-block describe how we got here.
            // We've got no style!
            // One is the minimum allowed for foo
            foo = 1;
        }
    }
```

Note that  you'll want an empty line (vertical space) above
inline comments. Exceptions are the first line in a method and the first
line in an `if-statement`. 

### TODO Comments
Often times your code will come with `TODO` comments that are helpful
in directing you what you should do. When your code doesn't work, often times
it is because some **TODO** has yet to be done. This is frequently done in
the industry and VS Code will event highlight these comments in the editor.  

```{admonition} Delete TODOs
:class: important
Once a task has been done and the **TODO** is no longer something that is
necessary to be done, delete the TODO comment!
```{code-block} java
:class: bad-code
// TODO: If you leave this comment in, you'll lose points!
System.out.println("Turn in clean code.");
```
### Header and Class Comment

You should have two comments at the beginning of your file before your
program. The first is the **header comment**, which provides identifying
information about you as the author of the program, similar to a header
you would write for an essay. You should include your name, the date,
the class (CSS 143), your TA's name, and the name of the program (the
assignment). The second is a **class comment** that provides a
high-level description of what your program does. An important thing to
remember is that your class comment should only describe what your
program does, not how it does it. A client of your code doesn't care
and shouldn't need to know how your code works (ie. using
Scanners/PrintStreams, some sort of loop or conditional structure, class
constants, etc.). Including these *implementation details* in your
comment also makes it difficult to change your code later on and still
have accurate comments. Omitting implementation details allows you to
change how you implement your code without having to change your
documentation. An example of a good class header could be:

```{code-block} java
:class: good-code
// Student Studentname
// 11.20.2025
// CSS 143 Section XX

import java.util.*;
import java.io.*;

// IMDB Search
// Searches a text file containing information about the top 250
// rated movies on IMDB for movies containing a particular word in the title,
// then prints the results to an output file.
public class ImdbSearch {
    // ...
}
```

### JavaDocs
[JavaDoc commenting](https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html) is rarely required. You will know when it is required. However, you
are welcome to use it at anytime. 
```{code-block} java
:class: good-code

    /**
     * Comment what this method does here. Don't say how!
     *
     * @param questionIndex The index into the question we want the answer for.
     * @param jitter How much randomization to provide in the answer.
     * @return The answer to the question.
     */
    public String getAnswer(int questionIndex, double jitter) {
        // Inline comment here
    }
```
> This style of commenting is called Javadoc notation. Javadoc uses
> multi-line comments that start with `/**`. Javadoc gives you a really
> nice template for commenting, but is not always necessary for your
> comments in this class. Javadoc also allows you to generate
> documentation files for your program similar to the official Java
> docs. You can do this in jGrasp by hitting the button that looks like
> an open book in the toolbar or from menus **File \> Generate
> Documentation**. You can learn more about Javadoc documentation
> [here](https://www.baeldung.com/javadoc){target="_blank"}.
### Let the Code Speak
You want to avoid useless comments that simply repeat what the code says.
```{code-block} java
:class: good-code
public class InterestCalculator {

    /**
     * Calculates compound interest.
     */
    public double calculateCompoundInterest(double principal, double rate, int years) {
        // Use the formula: A = P * (1 + r)^t
        return principal * Math.pow(1 + rate, years);
    }
}
```

```{code-block} java
:class: bad-code
// These comments just repeat what the code says. They don’t add insight.
// Don't comment the obvious. Let the code speak for itself.
public class InterestCalculator {

    /**
     * This method will make use of the Math class to do exponentiation while
     * calculating compound interest.
     */
    public double calculateCompoundInterest(double principal, double rate, int years) {
        // if rate is zero, just return principle
        if (rate == 0) {
            return principal;
        }

        // Print out the rate
        System.out.println(rate);

        // Multiply principal by (1 + rate) raised to the power of years,
        // then return this value.
        return principal * Math.pow(1 + rate, years);
    }
```
### Class Comments for Objects 

Objects are classes just like other code, but they represent something -
some object. So just like any other class, you should have a class
comment that describes what your class represents - in the case of an
Object, what it represents. Your class comments for some objects may be
shorter than some of the class comments you've written for other
programs - this is probably fine, as long as your class comment is
describing what the class represents. For example, for the Point class,
a complete class comment could be:

```{code-block} java
:class: good-code
// <header comment>
// A class to represent a point on the x-y coordinate plane.
public class Point {...}
```

### Method Comments 

You should include a comment for every method in your program, except
main (main should be a concise summary of the program, and your class
comment should already describe what your program does). A method
comment should describe what a method does, information about the
parameters it takes (if it takes parameters), and what is returned by
the method (if the method returns). For parameter comments, make sure to
explicitly name and describe the purpose of all parameters \-- what
information does this parameter provide? Think of commenting on
parameters as providing a brief definition.

> Note that just like with class comments, you should avoid talking
> about **implementation details** in your method comments for the same
> reasons. The client does not need to know how your method works and
> omitting implementation details allows you to change how you implement
> your code without changing your code documentation.

Take for example the method `roundN`

```{code-block} java
:class: bad-code
public static double roundN(double num, int digits) {
    return Math.round(num * Math.pow(10, digits)) / Math.pow(10, digits);
}
```

`roundN` rounds a given number to a given number of
digits (you don't need to understand anything about how this method
works, so it's fine if the method itself makes no sense to you right
now). Here are a few different styles of good, complete comments for
this method:

````{tab-set}
```{tab-item} Good #1
```{code-block} java
:class: good-code
// Rounds a given number num to the given number of digits and
// returns the rounded number
public static double roundN(double num, int digits) {...}
```
```{tab-item} Good #2
```{code-block} java
:class: good-code
// Rounds a given number to the given number of digits.
// Returns the rounded number.
// Parameters:
//    double num - the number to be rounded
//    int digits - the number of digits to round to
public static double roundN(double num, int digits) {...}
```
```{tab-item} Good #3
```{code-block} java
:class: good-code
/**
 * Rounds a given number to a given number of digits.
 * @param num - the number to be rounded
 * @param digits - the number of digits to round to
 * @return the rounded number
 */
public static double roundN(double num, int digits) {...}
```
````

### Instance Method Comments 

Instance methods are non-static methods that we declare in Object
classes. Just like any other method, instance methods should have method
comments that describe what the method does, what parameters the method
takes (if it takes any), and what the method returns (if it returns
anything). Take, for example the `fight` method from the Rabbit Critter.
Rabbits will attack using SCRATCH if the opponent is a Bird or a
Vulture:

```{code-block} java
:class: good-code
// Returns the Attack SCRATCH or ROAR based on the opponent:
// will SCRATCH if the opponent is a Bird or a Vulture, and ROAR otherwise
//      opponent - the String representation of the opponent Critter
public Attack fight(String opponent) {
    ...
}
```

### Constructor Comments 

Similar to instance methods, constructors *are* methods, they just
function a little differently than other methods. Just like any other
method, constructors should have method comments that describe what the
method does (usually just constructing that object, and any other
important behavior of the constructor), and what parameters the
constructor takes (if it takes any). Note that constructors do not
return anything, so there's no need for a return comment. Take, for
example the constructor for the Frog Critter. Frogs take an age as a
parameter that represents how old the Frog is:

```{code-block} java
:class: good-code
// Constructs a new Frog
// Parameters:
//      age - determines the frogs movement
public Frog(int age) {
    ...
}
```


### Comment Templates 

> Note: You should replace any text surrounded by `<` and `>` with the
> relevant information for your program.


### Things to Avoid in Comments 
#### Language

There are some phrases you should avoid in your comments. Saying "this
method" or "this program" in a method or class comment does not add
any valuable information; we already know you're talking about the
method/program, so you should just say what it does. You should also
avoid saying that a method "should" do something. You should comment
on what your method does do, not what it should.

#### Implementation Details

As mentioned previously, you should never include **implementation
details** in class and method comments. The client does not need to know
how your code works, and omitting implementation details allows you to
change how you implement your code without changing your code
documentation. Here are some examples of things you should never include
in comments:

- Control structure usage (if, for, while)
- methods used
- *"static method"*
- *"calls"*
- *"loop"*
- *"class constant"*
- *"extends"*

Finally, you should absolutely never refer to the spec in your comments.
The spec is for you, and you should assume that a client of your program
has no knowledge of it. We also hope that this is clear, but your
comments should be your description of your program, so copying text
verbatim from the spec **is considered academic misconduct and not
allowed**.

## Forbidden Features 
Don't use anything you don't understand. 

**The following features should NEVER be used in any assignment
(unless otherwise specified by the assignment or problem):**

- the `System.exit` method
- annotations
- the `<>` operator
- the `var` keyword
- Functional features (e.g., lambdas, streams, method references)
- the `toCharArray`, `join`, and `matches` methods of String


(Don't worry if you are not familiar with one of the features listed
above. You can simply think of these as Java features we have chosen not
to teach in this class so that we can focus on other important concepts
instead.)
