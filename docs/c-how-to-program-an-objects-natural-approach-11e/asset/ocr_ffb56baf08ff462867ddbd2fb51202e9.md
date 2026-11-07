```
```cpp
59    pop(heapVector);  // remove max item
60    pop(heapVector);  // remove max item
61    pop(heapVector);  // remove max item
62    std::cout << '\n';
63 }
```
```

```
```
popping highest priority item: 77
heap: 22 3

popping highest priority item: 22
heap: 3

popping highest priority item: 3
heap:
```
```

# ## 14.5 Function Objects (Functors)

As we’ve shown, many standard library algorithms allow you to pass a lambda or a function pointer into the algorithm to help it perform its task. Any standard library algorithm that can receive a lambda or function pointer can also receive a function object (also called a functor)—that is, an object of a class that overloads the function-call operator (parentheses) with a function named **operator()**. The overloaded **operator()** must meet the algorithm’s requirements for the number of parameters and the return type.

Function objects can be used syntactically and semantically like a lambda or a function pointer. The **operator()** function is invoked using the object’s name followed by parentheses containing the arguments. Most algorithms can use lambdas, function pointers and function objects interchangeably.

# ### Benefits of Function Objects

Function objects provide several benefits over functions and pointers to functions:

+   - A function object is an object of a class, so it can contain non-static data to maintain state for a specific function object or static data to maintain state shared by all function objects of that class type. Also, the class type of a function object can be used as a default type argument for template type parameters.

+   - Perhaps most importantly, the compiler can inline function objects for performance. A function object’s **operator()** function is typically defined in its class’s body, making it implicitly inline. When defined outside its class’s body, function **operator()** can be declared inline explicitly. Compilers implement lambdas as function objects, so these, too, can be inlined. On the other hand, compilers typically do not inline functions invoked via function pointers—such pointers could be aimed at any function with the appropriate parameters and return type, so a compiler does not know which function to inline.

27. “Function Objects in the C++ Standard Library,” March 15, 2019. Accessed April 18, 2023. https://docs.microsoft.com/en-us/cpp/standard-library/function-objects-in-the-stl.

28. Scott Meyers. *Effective STL: 50 Specific Ways to Improve Your Use of the Standard Template Library*. 201–202. Pearson Education, 2001.