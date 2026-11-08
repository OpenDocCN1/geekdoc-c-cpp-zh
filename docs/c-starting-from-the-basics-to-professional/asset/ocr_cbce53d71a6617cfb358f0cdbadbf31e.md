+   - You can take advantage of the multiprocessing capabilities of current hardware by passing the `std::execution::par` execution policy as the first argument to most (iterator pair-based) algorithms.
+   - In C++20 most algorithms in the `std` namespace received counterparts in the `std::ranges` namespace that allow you to directly manipulate ranges instead of iterator pairs.
+   - The `<ranges>` module introduces various views, as well as the means to easily produce and compose them. Views produced when piping a range adaptor alter the way the next stage in your algorithm perceives a range: they may transform elements, filter out elements, or rearrange them. Views produced by range factories generate new elements on the fly. Creating views and passing them around is very cheap: views and/or their elements are lazily generated.

# EXERCISES

The following exercises enable you to try what you've learned in this chapter. If you get stuck, look back over the chapter for help. If you're still stuck after that, you can download the solutions from the Apress website (www.apress.com/book/download.html), but that really should be a last resort.

Exercise 20-1. In practice, we would never recommend you to implement your own linked list data structure to store boxes in Truckload. At the time it made perfect sense to practice nested classes and working with pointers; but normally you should follow our advice from earlier in this chapter and simply use a `vector<>` instead (a polymorphic `vector<>`, to be precise—see Chapter 15). If you need a sequence container, a `vector<>` is almost always the way to go! Eliminate the linked list from the Truckload class of Exercise 18-1 according to this guideline. Notice how you can now adhere to the rule of zero as well (see Chapter 18)?

Exercise 20-2. Replace both instances of your self-defined `Stack<>` in Ex17_04A with an instance of `std::stack<>`.

Exercise 20-3. Rework your solution to Exercise 17-6 by replacing all instances of your `SparseArray<>` and linked list template types with standard containers. Carefully think about which container types would be most appropriate!

> **Note**  If you want extra practice, you can do the same for the solutions of Exercises 17-4 and 17-5 as well.

Exercise 20-4. Research the `partition()` algorithms and use one to reimplement the `removeEvenNumbers()` function of either Ex20_10 or Ex20_14.

Exercise 20-5. Not all Standard Library algorithms are defined by the `<algorithms>` module. Some are defined by the `<numerics>` module as well. One such example is `accumulate()`. Research this algorithm and use it to implement an algorithm-like function template that computes the average of a given iterator range. Exercise your newly implemented template with a little test program.