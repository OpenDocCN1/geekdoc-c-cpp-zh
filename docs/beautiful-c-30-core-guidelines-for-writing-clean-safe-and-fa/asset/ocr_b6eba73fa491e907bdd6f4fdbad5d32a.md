# Working further from the metal

Things are different for me now. C++ takes me very close to the metal, but not on the metal. The compiler bridges that gap and embodies all the detailed knowledge that I used to have about the Z80 processor. In my current case that knowledge concerns the x86-64 architecture, which encompasses multiple processors. I cannot hope to acquire the necessary detail on my own. This is one of the reasons for moving to C++.

There is an art to optimization, but there is also an art to developing code that can be optimized well. You cannot optimize code that is utterly inflexible, and opti-mized code will often end up in this state. Optimizable code leaves options for the optimizer, be that a human or a compiler. Code that can be optimized is code with options to change things. Indeed, the words “optimize” and “option” both have the same Latin root, optare, “to choose.”

Engineers tend to optimize code in two ways, either by improving the design or by improving the performance. Improving the design means improving the compre-hensibility and reusability of the code or responding to refinements to the require-ments. Improving the performance means giving the compiler the greatest amount of information about what it is that you want to do and the greatest range of options to improve the performance.

The Core Guidelines page offers a good example from the C standard, which we reproduce here:

Click here to view code image

```
void qsort(void* base, size_t num, size_t size,
    int(*comp)(const void*, const void*));
```

This function takes a pointer to some memory, the number of things you want to sort, the size of the things you want to sort, and a function for ordering the things you want to sort.

Let’s start with optimizing the design of this function. The first problem is that we seem to be sorting memory rather than sorting things. This is the wrong level of abstraction. If you’re going to name a function “sort,” then the implication is that you will be sorting things. The idea of sorting