# # 12

# # Classes and Dynamic Memory Allocation

In this chapter you'll learn about the following:

+   - Using dynamic memory allocation for class members
+   - Implicit and explicit copy constructors
+   - Implicit and explicit overloaded assignment operators
+   - What you must do if you use `new` in a constructor
+   - Using `static` class members
+   - Using placement `new` with objects
+   - Using pointers to objects
+   - Implementing a queue abstract data type (ADT)

This chapter looks at how to use `new` and `delete` with classes and how to deal with some of the subtle problems that using dynamic memory can cause. This may sound like a short list of topics, but these topics affect constructor design, destructor design, and operator overloading.

Let's look at a specific example of how C++ can add to your memory load. Suppose you want to create a class with a member that represents someone's last name. The simplest, most primitive way is to use a character array member to hold the name. But this has some drawbacks. You might use a 14-character array and then run into Bartholomew Smedsbury-Crawthingham. Or to be safer, you might use a 40-character array. But if you then create an array of 2,000 such objects, you'll waste a lot of memory with character arrays that are only partly filled. (At that point, you're adding to the computer's memory load.) There is an alternative.

Often it is much better to decide many matters, such as how much storage to use, when a program runs rather than when it's compiled. The usual C++ approach to storing a name in an object is to use the `new` operator in a class constructor to allocate the correct amount of memory while the program is running. The usual way to accomplish this is to