# Reversing Randomized Response

Before you read this, please read the background found <a href='https://cse163.github.io/book/module-10-beyond-163/lesson-29-privacy/randomized-response.html' target='_blank'>in our online book.</a>

Here we discuss how to get an understanding of the actual number of `yesses` and `nos` from the randomized response.  

You might be thinking, only the people who flipped heads are telling us the truth, how are we going to get an accurate answer with just 50% percent of the population telling us the truth? The answer to that question involves some simple math and statistics.  

With the randomized response technique, 3/4 of the population will tell us the truth, either due to the first coin toss or "accidentally" with the second coin toss. If a person gets heads on their first flip, they tell the truth, so that is 50% of the population telling us the truth. If they flip tails, then we get a 50-50 chance that they are telling us the truth, so that leaves us with 25% of the remaining population telling us the truth, and the other 25% telling us a lie. 

TODO: Illustrations and dialog coming soon.  

Now that we have figured out the range that it can be in, we can narrow it down and get a reasonable range where we can reach a conclusion. To reduce our range, we will use the **binomial standard deviation formula** 

Binomial Standard Deviation Formula: $\sigma = \sqrt{n \cdot p \cdot (1 - p)}$ 

TODO: More explanation coming.  
