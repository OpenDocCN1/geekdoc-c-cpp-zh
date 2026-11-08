
- You can take advantage of the multiprocessing capabilities of current hardware by passing the `std::execution::par` execution policy as the first argument to most (iterator pair-based) algorithms.
- In C++20 most algorithms in the `std` namespace received counterparts in the `std::ranges` namespace that allow you to directly manipulate ranges instead of iterator pairs.
- The `<ranges>` module introduces various views, as well as the means to easily produce and compose them. Views produced when piping a range adaptor alter the way the next stage in your algorithm perceives a range: they may transform elements, filter out elements, or rearrange them. Views produced by range factories generate new elements on the fly. Creating views and passing them around is very cheap: views and/or their elements are lazily generated.

## EXERCISES

The following exercises enable you to try what you've learned in this chapter. If you get stuck, look back over the chapter for help. If you're still stuck after that, you can download the solutions from the Apress website (www.apress.com/book/download.html), but that really should be a last resort.

- Exercise 20-1. In practice, we would never recommend you to implement your own linked list data structure to store boxes in Truckload. At the time it made perfect sense to practice nested classes and working with pointers; but normally you should follow our advice from earlier in this chapter and simply use a `vector<>` instead (a polymorphic `vector<>`, to be precise—see Chapter 15). If you need a sequence container, a `vector<>` is almost always the way to go! Eliminate the linked list from the Truckload class of Exercise 18-1 according to this guideline. Notice how you can now adhere to the rule of zero as well (see Chapter 18)?

- Exercise 20-2. Replace both instances of your self-defined `Stack<>` in Ex17_04A with an instance of `std::stack<>`.

- Exercise 20-3. Rework your solution to Exercise 17-6 by replacing all instances of your `SparseArray<>` and linked list template types with standard containers. Carefully think about which container types would be most appropriate!

> **Note** If you want extra practice, you can do the same for the solutions of Exercises 17-4 and 17-5 as well.

- Exercise 20-4. Research the `partition()` algorithms and use one to reimplement the `removeEvenNumbers()` function of either Ex20_10 or Ex20_14.

- Exercise 20-5. Not all Standard Library algorithms are defined by the `<algorithm>` module. Some are defined by the `<numeric>` module as well. One such example is `accumulate()`. Research this algorithm and use it to implement an algorithm-like function template that computes the average of a given iterator range. Exercise your newly implemented template with a little test program.

- Exercise 20-6. Another algorithm that is defined by the `<numeric>` module is the `iota()` algorithm, which you can use to fill a given range with values M, M+1, M+2, and so on. Use it to rework the `fillVector_iotaN()` function of Ex20_10.

- Exercise 20-7. Speaking of Ex20_10, you of course know that instead of filling a vector of values ranging from 1 to M, you could have used an appropriate view. And instead of removing elements from that vector, you could have used another view. Rework Ex20_10 to work with views.

- Exercise 20-8. `erase()` and `erase_if()` are not the only algorithms for which the remove-erase idiom is applicable. Another example is `std::unique()`, which is used to remove duplicates from a presorted range of elements. Write a little program that fills a `vector<>` with a considerably large amount of random integers between 0 and 10'000, sorts this sequence, removes the duplicates, and then prints out the amount of remaining elements.

- Exercise 20-9. Parallelize your solution to the previous exercise.

- Exercise 20-10. Near the end of Ex20_15A we sort a range of strings on their length. Come up with two different ways to rewrite this algorithm invocation. You are not allowed to (directly) use the `<` operator anymore for this. (And, no, that does not mean you should use `<=>` instead, or use `>` and then `reverse(...)`).

- Exercise 20-11. Write a function that determines whether a given integer is a prime number. If you're lost on how to do this, you can always distill a prime test from Ex6_05. Now use this function to print out the first 100 prime numbers in reverse order. Do so without the use of any container.

  Hint: You already used the `iota(from,to)` range factory, but `iota(from)` is valid as well. The latter factory call produces a view that, conceptually, contains an infinite amount of consecutive values, starting with `from`. Because a view's elements are only generated lazily, having a view that is, at least conceptually, infinitely large is no problem. Just make sure you do not attempt to exhaustively read all elements of such a view because that might take a while...

- Exercise 20-12. Research the `take_while()` and `drop_while()` range adaptors and use them to alter your solution to Exercise 20-11 to output all prime numbers smaller than 1,000.

- Exercise 20-13. Replace the loop in the `maxWordLength()` function of Ex20_05 with an appropriate algorithm. Try to come up with a few alternative solutions.

- Exercise 20-14. We’ll end this chapter with a harder nut to crack. Ask the user to input a sequence of numbers, each one followed by Enter. After each number, print out “Yes, that is a prime!” when it is a prime number. You do not print anything if it is not a prime number. You can stop the program as soon as the user enters a negative number. Not that hard a nut, you say? Then here comes the twist: You are not allowed to use any container, if statement, or loop. Not even to determine whether a number is prime. You have to accomplish everything using algorithms, view adaptors, and view factories.

  Hint: Perhaps look into `std::ranges::istream_view<int>(std::cin)`? And if you want to avoid the use of a `for_each()` algorithm (because that’s just cheating, right?), perhaps look into the special output iterator `std::ostream_iterator`?

## CHAPTER 21
## Constrained Templates and Concepts

Templates define parameterized families of C++ entities such as functions (Chapter 10) or class types (Chapter 17). In practice, templates are mostly parameterized on seemingly arbitrary types. Yet most templates cannot be instantiated for just any type; at least not without error. The binary `std::max<>()` function template, for instance, can only be instantiated for types that support the `<` operator. And the `std::vector<>` and `std::optional<>` class templates may not be instantiated for reference types, `void`, or array types. Most of your own templates have similar restrictions as well, whether you realized it or not.

One thing all these templates have in common is that the restrictions on their template type arguments are all *implicit* and stem from how values of dependent types are used, often deep inside the templates' code. There is nothing *explicitly* preventing you from invoking `max<>()` for values without a `<` operator, or from attempting to create objects of types such as `vector<int[]>` or `optional<int&>`. It's just that doing so will result in a flood of often-incomprehensible template instantiation errors. And without any indication in a template's head, how are you supposed to know what parameters can and cannot be used? Short of dissecting the template's code, your best bet is to look for code comments or online API documentation—which as we all know are often lacking.

In this chapter, you'll learn

- What a concept is and what the qualities are of well-designed concepts
- How to define your own concepts
- How to work with the concepts that the Standard Library has to offer
- How to explicitly encode restrictions on template type parameters using constraints and why doing so makes your templates easier to use
- What constraint-based template specialization is and how it allows you to specialize your algorithms or data structures for select families of types
- That concepts can be used outside of the context of templates to constrain placeholder types such as `auto`, `auto*`, `const auto&`

All language and library features you learn about in this chapter are new in C++20.
