# CHAPTER 17

![](bbox=[0.196, 0.212, 0.254, 0.225])

# # Class Templates

Both function and class templates are used extensively throughout the C++ Standard Library to provide powerful generic utilities, algorithms, and data structures. You learned about templates that the compiler uses to create functions in Chapter 10; this chapter is about templates that the compiler uses to create classes. Class templates are a powerful mechanism for generating new class types.

With this chapter, you are also nearing the end of our series of chapters on defining your own classes. Besides introducing class templates we will therefore also include some slightly off-topic contemplations on coding style. With these sidebars we want to entice you to reason about aspects of your code that go beyond mere functional correctness. We will advocate that writing code should be about more than just making sure it computes the correct values. Your code should be easy to read and maintain, it should be robust against unexpected conditions and exceptions, and so on. Naturally, we will also teach you a few standard techniques along the way to help you accomplish these fundamental nonfunctional requirements.

+   - What a class template is and how to define one
+   - What an instance of a class template is and how it is created
+   - How to define templates for member functions of a class template outside the class template definition
+   - What a partial specialization of a class template is and how it is defined
+   - How a class can be nested inside a class template
+   - Why it pays to invest in high-quality code that is not just correct but also easy to maintain and robust against failure
+   - What the “copy-and-swap” idiom is and how to use it to write exception-safe code
+   - How to use the “const-and-back-again” idiom to avoid duplicating overloaded member functions

# ## Understanding Class Templates

A class template is based on the same idea as a function template (see Chapter 10). It is a parameterized type that constitutes a recipe for creating a family of class definitions. Just like a recipe is not edible, a class template definition in itself has no executable code associated with it. It’s only when the compiler instantiates concrete class definitions from a class template that it gives rise to actual code. Before your program can use variables of type std::vector<int>, for instance, the compiler has to instantiate a