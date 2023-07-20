# <i class="fas fa-laptop fa-fw"></i> HW6 - Spell Checker

**Learning objective:** Implement efficient code with generators. 

## Rubric & Submission
Please note these important things:
* You will NOT turn this into AutoGrader. You will **Submit to Replit.**
* This will be for your High School Grade only.  It will be worth `40 points` (40% a UW Homework Assignment).
* You will be graded on the Replit Unit Tests only. ~3pts per Unit Test.
* You will not be graded on any commenting or tests you write.
* Please know the due date and TIME as posted in Schoology. (6am Feb 3)


## Instructions  
In this project you will learn:  
* Class implementation (should just be extra practice by now)
* The importance of efficiency
* How to do implement spelling suggestions
* How to do implement a `generator`

All of these things will accomplished by implementing a `SpellChecker` class.

Your Spell Checker program will be giving a list of words to use as its dictionary.
The primary pieces of functionality will be to:  
* Determine if a single word is misspelled
* Find all the misspelled words in an _essay_ (text file)  
* Provide a set of correctly spelled words as suggested corrections

A basic infrastructure of the SpellChecker class will be provided. 

## Spell Checking an Essay
First, improve the code so that it can complete the spell checking quickly.

You will implement the following three things in the class `SpellChecker`:
1) `constructor` : Takes the name of a dictionary and intializes a SpellChecker object.  
2) `misspelled` : An instance method that returns True if the word passed in is not found in the dictionary.
3) `spell_check` : An instance method that returns a list of misspelled words found in the essay while also outputting to the console details about which words are misspelled.

There are several Unit Tests that related to the above that you should pass
before continuing onto the next step. Note that these Unit Test will test both
the functionality as well as the speed of execution. You need to have _FAST_ code!!

Also, the output printed to the console for `spell_check` should look close to:

```
civalized: line: 1  word:3
oportunities: line: 6  word:4
seeems: line: 15  word:9
peopl: line: 21  word:8
ettiquitt: line: 35  word:1
shoudl: line: 37  word:7
psudo-code: line: 37  word:10
algorythm: line: 39  word:6
```

Be sure you Pass the Unit Tests:  
* test_misspelled
* test_check_essay
* test_check_essay_speed_not_garbage
* test_check_essay_speed_okay
* test_check_essay_speed_good

### Tips for Passing Test
Make sure that you have your own tests written. You will understand the input
and expected output of your own tests. This will assure that things are working
according to plan. 

> Mr. Stride will ask to see your tests first before helping you figure out why
> a functional Unit Test is failing.

You need to update `misspelled` to work with hyphenated words. There is
a slick and easy recursive approach to this which is also very fast.  
> Hint: If no hyphen, solve normally. If it has hyphens, break into subwords
> and solve for each subword.

`misspelled` needs to work with hyphenated words with multiple hyphens!
> Example: `word-is-good-now` is correctly spelled!  

If you are not passing the speed checks, it could be several things:
* Maybe Mr. Stride's test are bad. Do other students' tests pass?
* Verify that the data structure you're using to hold the dictionary is fast.

## Generators
Before we move onto the next phase of development, you need to learn about
`generators`.   

In Python, a generator is a special type of function that produces a sequence 
of values, one at a time, when iterated over. Generators are different from 
regular functions in that they do not return all their output at once; instead, 
they `yield` their values one at a time, which allows them to be more memory-efficient 
than regular functions that return all their output at once.  

Here is a simple example of a generator in Python:

```python
def countdown(n):
    while n > 0:
        yield n
        n -= 1

for i in countdown(5):
    print(i)
```
This generator, countdown, yields the values 5, 4, 3, 2, and 1, one at a time, 
when it is iterated over. When the generator is called, it does not execute the 
code inside of it immediately; instead, it returns a special type of iterator 
called a "generator iterator", which can be used to execute the code in the 
generator one step at a time.

Generators can be very useful for producing large sequences of data, because 
they allow you to generate the values one at a time, rather than creating a 
list with all the values at once, which can be very memory-intensive.

Here are a couple of YouTube videos that explain generators in Python:

* [Python Generators: (By Socratica)](https://www.youtube.com/watch?v=gMompY5MyPg)  
* [Python Generators Explained (With Examples) (By Corey Schafer)](https://www.youtube.com/watch?v=bD05uGo_sVI)

These videos provide a good overview of generators, including how to create them, 
how to use them, and some of the benefits of using generators in your Python code.

## Spelling Suggestion
This is where the project starts to get more interesting. There are many creative ways 
to suggest words for a misspelled word.
We will start simple and then build up to _AMAZING!_

### Mis-misspelled
We will start with a concept that I'll call: `mis-misspelled`. The basic idea 
is that we will modify the spelling of a misspelled word until
it is modified into a correctly spelled word.  

For example: Let's consider the misspelled word, `aple`. If we modify `aple` by 
introducing another `p` into the '3rd' position (after the second letter) then
we will generate the word `apple` which is correctly spelled! 

Using this concept, we could have the following code:   
```python
def get_suggestion(self, misspelled_word):
    for mis_misspelled_word in create_misspelling(misspelled_word):
        if not misspelled(mis_misspelled_word):
            return mis_misspelled_word
```

> For each section below, attempt find the correct spelling for words
using the generator just created.

### Part 1
You will implement a create_misspelling `generator`, but instead of using the name 'create_misspelling',
we will use a more specific name that describes exactly _how_ we are misspelling the
word. Let's name it: `_insert_letters`. 
> Note: we prefix the name with `_` because it is a private method. Also, this
> method is an instance method (belongs to the object).

This method will insert all the letters, a-z, into every possible
position of a given word. 

Be sure you pass the Unit Test:  
* test_insert_letters

### Part 2
Implement another generator to move all letters, one letter at a time. 
This will be called: `_remove_letters`. For example: 
```python
   for word in self._remove_letters('goodbye'):
      print(word)

# prints
oodbye
godbye
godbye
goodye
goodbe
goodby
```

Be sure you pass the Unit Test:  
* test_remove_letters
  
### Part 3
Implement another generator to change all letters, one letter at a time. 
This will be called: `_swap_letters`. Note that this does NOT mean that
two letters in the word is swapped. Instead, it means that one letter is
swapped out for another. For example: 
```python
   for word in self._swap_letters('ab'):
      print(word)

# optionally prints 'ab', but definitely prints...
bb
cb
db
eb
fb
gb
...
yb
zb
aa
ac
ad
ae
af
ag
...
ay
az

```

Be sure you pass the Unit Test:  
* test_swap_letters

## suggest_correction
It is time to implement the method `suggest_correction`. This method
should return a list of suggested words that could be the correct
spelling for the misspelled word. The list will have an maximum number
of words added to the list which is specified in the optional `max` argument.

```python
    def suggest_correction(self, word, max=6):
        # student's implementation goes here
```
### Composing
Each `generator` above catches some types of mistakes, but not all of them.
In fact, you can't even try all three back-to-back-to-back because some
misspelled words require ALL THREE at the SAME TIME!! For example, to
identify the correctly spelled word `etiquette` from `ettiquitt` requires
that we delete a `t`, add an `e`, and change an `i` to an `e`. All three!!

We want to implement all 3 types, composed with one another. This can be
difficult. Here is a way to compose all three together:
```python
    def suggest_correction(self, word, max=6):
        # partial implementation only!!
        fns = [self._insert_letters, self._remove_letters, self._swap_letters]
        for word in self._compose_fns(word, fns):
            # rest of code not shown

    def _compose_fns(self, word, fns):
        ''' 
        A recursive generator that composes all the generators in fns.
        word : the word that is misspelled
        fns : a list of generators
        '''
        for fn1_word in fns[0](word):
            yield fn1_word
            if len(fns) == 1:
                yield fn1_word
            else:
                # our recursive case must be in the form of a for-loop
                for fn2_word in self._compose_fns(fn1_word, fns[1:]):
                    yield fn2_word
```
Be sure you pass the Unit Test:  
* test_suggest_compose : This tests that suggest_correction correctly finds a suggestion for a misspelled word that requires three changes.
  
Using the above code, see if you can correctly produce at least one suggestion
for each of the misspelled words in `englishEssay.txt`.  

> Note: Your code may run for as much as a full minute to find suggestions for all
> the misspelled words in the englishEssay.txt.

## Levenshtein Distance
There are two problems with what we've done so far:  
1) It's too slow!!
2) The list may contain lots of odd words

We are going to change the approach to solving this Suggestion Problem. We
will essentially go backwards. Instead of generating mis-misspelled candidates
and then search the dictionary to see if it is indeed a correctly spelled word,
we will compare 'every' word in the dictionary against the misspelled word
to see if it is 'close'. The 'closests' words will be what we suggest.

To accomplish this, we need a way to _measure the 'distance'_ between two words. 
The Levenshtein Distance algorithm is exactly what we want. The algorithm will
provide an integer number that is essentially the count of changes made to one
word to reach the other. The changes are exactly the same three generators you
implemented above. (The algorithm will not use your generators.)

You will add a new instance method to the SpellChecker class.
```python
    def lev_suggest_correction(self, word):
       '''
       Return a list of all the suggest words that share the same, minimum
       distance from word using the levenshtein distance algorithm.
       '''
```

It can take a while to understand the algorithm which can take us off topic
quite a bit. So, instead, you have been provided with three different implementations
of the algorithm in the file `levenshtein.py`.

Below are the names of the 3 implementations along with the time (in seconds) it took to provide
suggestions for all the misspelled words in the englishEssay.txt. (Times were using
Mr. Stride's implementation. Measured only once.)

1) `levenshtein_distance: 71.16`
2) `lev_distance:         51.45`
3) `fast_lev_distance:     1.42`

It is pretty clear that one implementation is much, much, much faster than the rest.
This is because it is implemented in the Python module [editdistance](https://pypi.org/project/editdistance/)
written in C++. Because it is written in C++ the code can run a lot faster.
Furthermore, some braniacs out there used some fancy math an algorithm techniques
to speed it up even more. 

### Experience the Difference
Implement the `lev_suggest_correction` and experience the difference in speed
from one algorithm to the other. Amazing, right?!

Be sure you pass the final two Unit Tests:

