The book therefore contains the following parts:

+   - **Part I** covers the basic features of move semantics (especially for non-generic code).

+   - **Part II** covers the features of move semantics for generic code (especially used in templates and generic lambdas).

+   - **Part III** covers the use of move semantics in the C++ standard library (giving also a good example of how to use move semantics in practice).

# How to Read This Book

Do not be afraid by the number of pages in this book. As always with C++, things can become pretty complicated when you look into details (such as implementing templates). For a basic understanding, the first third of the book (Part I, especially chapters 1 to 5) is sufficient.

In my experience, the best way to learn something new is to look at examples. Therefore, you will find a lot of examples throughout the book. Some are just a few lines of code illustrating an abstract concept, whereas others are complete programs that provide a concrete application of the material. The latter kind of examples will be introduced by a C++ comment describing the file containing the program code. You can find these files on the website for this book at http://www.cppmove.com.

# The Way I Implement

Note the following hints about the way I write code and comments.

# Initializations

I usually use the modern form of initialization (introduced in C++11 as *uniform initialization*) with curly braces:

```
int i{42};
std::string s{"hello"};
```

This form of initialization, which is called *brace initialization*, has the following advantages:

+   - It can be used with fundamental types, class types, aggregates, enumeration types, and auto

+   - It can be used to initialize containers with multiple values

+   - It can detect narrowing errors (e.g., initialization of an int by a floating-point value)

+   - It cannot be confused with function declarations or calls

If the braces are empty, the default constructors of (sub)objects are called and fundamental data types are guaranteed to be initialized with 0/false/nullptr.