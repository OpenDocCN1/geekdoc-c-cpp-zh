+   - All string objects have member functions, including those for determining a string object's length, determining whether or not a string object is empty, finding substrings, and removing substrings.
+   - Arrays provide a way to store and access sequences of any type.
+   - A limitation of arrays is that they have a fixed length.
+   - You can access individual elements of string objects and arrays through the subscripting operator.
+   - Bounds checking is not enforced when attempts are made to access individual elements of string objects or arrays. Therefore, bounds checking is up to the programmer.
+   - C-style strings are character arrays terminated with the null character. They are the standard way to represent strings in the C language. And even though C-style strings are perfectly legal in C++, string objects are the preferred way to work with sequences of characters.
+   - Multidimensional arrays allow for access to array elements using multiple subscripts. For example, a chessboard can be represented as a two-dimensional array, 8 × 8 elements.

# QUESTIONS AND ANSWERS

Q: Which is better, a while loop or a for loop?
A: Neither is inherently better than the other. Use the loop that best fits your needs.

Q: When might it be better to use a for loop than a while loop?
A: You can create a while loop to do the job of any for loop; however, there are some cases that cry out for a for loop. Those include counting and iterating through a sequence.

Q: Can I use break and continue statements with for loops?
A: Sure. And they behave just like they do in while loops: break ends the loop and continue jumps control back to the top of the loop.

Q: Why do programmers tend to use variable names such as i, j, and k as counters in for loops?