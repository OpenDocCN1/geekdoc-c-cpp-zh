In this case, the example creates a vector, MyVector, and populates it with data. It then calls ProcessVector() to perform a task with the data in the vector.

The call to ProcessVector() creates a functor — a special class of object that acts as if it's a function — named Func. This is an extremely useful kind of a class that you explore further in the “Functors” section of Book VI, Chapter 1. For now, all you need to know is that it's a special kind of a class that acts like a function.

The for_each() algorithm (demonstrated fully in the “Creating Improved Loops Using Foreach” section of Book VI, Chapter 5) is part of the standard library. It processes each element in vect, the vector passed to ProcessVector(), starting at the first element (defined by vect.begin()) and ending with the last element (defined by vect.end()) using Func.

When you look at MyFunctor, you see a definition for an operator that requires a single int input, x. All that the code does is output x to the console. So you see the following output from this example.

```
1
2
3
4
```

# # Defining the Essential Lambda Expression

The intent of a lambda expression is to make code shorter and easier to read. It creates a new method for presenting code. However, it doesn't actually create a new C++ capability. What you're doing is using the same techniques, but in a different manner than before. The following sections help you create your first lambda expressions so that you get a better idea of precisely how they work.

# ## Defining the parts of a lambda expression

The example in the previous section is perfectly usable. However, the functor is only used one time in the example. This situation happens relatively often and it causes confusion for developers who need to work through the resulting code. A lambda expression makes it possible to incorporate the functor as part of the for_each() algorithm, as shown in the Solution example in Listing 7-2.

Book IV
Chapter 7
Working with
Lambda Expressions