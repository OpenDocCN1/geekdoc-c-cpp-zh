# 26.1 What we want

Let’s try a simple experiment. Write a binary search. Do it now. Don’t wait until the end of the chapter. Don’t wait until after the next section. It’s important that you try. Now! A binary search is a search in a sorted sequence that starts at the middle:

+   - If the middle element is equal to what we are searching for, we are finished.
- If the middle element is less than what we are searching for, we look at the right-hand half, doing a binary search on that.
- If the middle element is greater than what we are searching for, we look at the left-hand half, doing a binary search on that.
- The result is an indicator of whether the search was successful and something that allows us to modify the element, if found, such as an index, a pointer, or an iterator.

Use less than (<) as the comparison (sorting) criterion. Feel free to use any data structure you like, any calling conventions you like, and any way of returning the result that you like, but do write the search code yourself. In this rare case, using someone else’s function is counterproductive, even with proper acknowledgment. In particular, don’t use the standard library algorithm (binary_search or equal_range) that would have been your first choice in most situations. Take as much time as you like.

So now you have written your binary search function. If not, go back to the previous paragraph. How do you know that your search function is correct? If you haven’t already, write down why you are convinced that this code is correct. How confident are you about your reasoning? Are there parts of your argument that might be weak?