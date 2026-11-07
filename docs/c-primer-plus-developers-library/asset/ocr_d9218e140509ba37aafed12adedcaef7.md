Here is a sample output:

```
    Sample size = 390000
    Count of numbers divisible by 3: 130274
    Count of numbers divisible by 13: 30009
    Count of numbers divisible by 3: 130274
    Count of numbers divisible by 13: 30009
```

It's reassuring that both approaches (two separate lambdas and a single lambda) in this program led to the same answers.

The main motivation for adding lambdas to C++ was to enable using a function-like expression as an argument to a function expecting a function pointer or functor as an argument. So the typical lambda would be a test expression or comparison expression that could be written as a single return statement. That keeps the lambda short and easy to understand and enables automatic deduction of the return value. However, it is likely that a subset of the ingenious C++ programming community will develop other uses.

# # Wrappers

C++ provides several *wrappers or adapters*. These are objects used to provide a more uniform or more appropriate interface for other programming elements. For example, Chapter 16 described `bind1st` and `bind2nd`, which adapt functions with two parameters to match up with STL algorithms that expect functions with one parameter to be supplied as an argument. C++11 provides additional wrappers. They include the `bind` template, which provides a more flexible alternative to `bind1st` and `bind2nd`, the `mem_fn` template, which allows a member function to pass as a regular function, the `reference_wrapper` template allows you to create an object that acts like reference but which can be copied, and the `function` wrapper, which provides a way to handle several function-like forms uniformly.

Let's look more closely at one example of wrapper, the *function* wrapper, and at the problem it addresses.

# ## The *function* Wrapper and Template Inefficiencies

Consider the following line of code:

```
`answer = ef(q);`
```

What is *ef*? It could be the name of a function. It could be a pointer to a function. It could be a function object. It could be a name assigned to a lambda expression. These all are examples of *callable types*. The abundance of callable types can lead to template inefficiencies. To see this, let's examine a simple case.

First, let's define some templates in a header file, as shown in Listing 18.6.