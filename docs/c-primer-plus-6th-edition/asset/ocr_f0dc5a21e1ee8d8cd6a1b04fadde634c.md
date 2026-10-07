What Now? 1207

```
Here are a couple of sample runs:

Enter your weight: 150
A 10% increase raises 150 to 165.

Enter your weight: 156
A 10% increase raises 156 to 171.600006.

The second sample run shows one of the limitations of lexical_cast;it doesn't pro-
vide control over floating-point formatting. To get that, you need to use the more
elaborate incorporate formatting facilities discussed in Chapter 17,"Input, Output, and Files.\nYou can also use lexical_cast to convert strings to numeric values.
viously, there is much, more to Boost. For example, the Any library allows
to store (recover) a heterogeneous collection of values and objects of different
types in an STL container, using the Any template as a wrapper for the various values.
The Boost Math library extends the list of functions beyond that of the standard math
library.The Boost Filesystem library facilitates code that is portable across plat-
using different file systems. You can refer to the Boost website (www.boost.org) to
get more information about the contents of the library and how to add it to various plat-
forms.Also any C++ distributions, such as the one from Cygwin, come with the Boost
library included.
```

# What Now?

If you worked your way through this book, you should have a good grasp of the
rules of C++. However, that's just the beginning in this learning language. The second
stage is learning to use the language effectively, and that is the longer journey. The best
stage is to be in a work or learning environment that brings you into contact with
good C++ code and programmers. Also now that you know C++, you can read books
that concentrate on more advanced topics and on object-oriented programming.
Appendix H, "Selected Readings and Internet Resources,"lists some of these resources.
One promise of OOP is to facilitate the development and enhance the reliability of
large projects. One of the essentials of the OOP approach is to invent the classes
that represent the system (called the problem domain) that you are modeling. Because real
problems are often complex, finding a suitable set of classes can be challenging. Creating a\complex system from scratch usually doesn't work; instead, it's best to take an iterative,
evolutionary approach. Toward this end, practitioners in the field have developed several
teiques and strategies. In particular, it is important to do as much of the iteration and
evolution in the analysis and design stages as instead of writing and rewriting
actual code.
Two common techniques are use-case analysis and CRC cards. In use-case analysis, the
development team lists the common ways, or scenarios, in which it expects the final sys-
t be identifying elements, actions, and responsibilities that suggest possible