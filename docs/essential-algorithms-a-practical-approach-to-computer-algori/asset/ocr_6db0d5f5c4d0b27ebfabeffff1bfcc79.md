The DoubleIt method takes an integer as a parameter and returns an integer. The code doubles the input value and returns the result. DoSomething method takes as a parameter an array of integers values. It performs a task and does not return a result. For example, it might randomize or sort the items in the array. (Note that this book assumes arrays start with the index 0. For example, an array containing three items has indices 0, 1, and 2).

Pseudocode is intuitive and easy to understand, but if you find something that doesn't sense to you, feel free to post a question on the discussion forum at www.wiley.com/essentialalgorithms or e-mail me RodStephens@CSharperHelper.com. I'll point you in the right direction.

One problem with pseudocode is that it has no compiler to detect errors. As a check of the basic algorithm, and to give you some actual code to use for a reference, C# implementations of the algorithms and many of the exercises are available for download on the book's website.

# Algorithm Features

A good algorithm must have three features: correctness, maintainability, and efficiency.

Obviously if an algorithm doesn't solve the problem for which was designed, it's not much use. If it doesn't produce correct answers, there's little point in using it.

> NOTE Interestingly, some algorithms produce correct answers only of the time but are still useful. For example, an algorithm may be able to give you some information with a certain probability. In that case you may be able to rerun the algorithm many times to increase your confidence that the answer is correct. Fermat's primality test, described in Chapter 2, is this kind of algorithm.

If an algorithm isn't maintainable, it's dangerous to use in a program. If an algorithm is simple, intuitive, and elegant, you can be confident that it is producing correct results, and you can fix it if it doesn't. If the algorithm is intricate, confusing, and convoluted, you may have a lot of trouble implementing it, and you will have even more trouble fixing it if a bug arises. If it's hard to understand, how can you know if it is producing correct results?

> NOTE This doesn't mean it isn't worth studying difficult algorithms. Even if you have trouble implementing an algorithm, you may learn a lot in the attempt. Over time your intuition and skill will increase, so algorithms you once thought confusing will seem easier to handle. You must always test all algorithms thoroughly, however, to make sure they are producing correct results.