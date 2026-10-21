# Chapter 8

The second part of the problem is solved using the three nested for loops iterating over the possible ranges of m_Length, m_Width and m_Height so that you evaluate all possible combinations. You could output them all as well, but because this would involve 200 combinations, of which you might only be interested in a few, you have an if statement that identifies the options that you’re actually interested in. The if expression is only true if there’s no space wasted in the carton and the current trial candy box has no wasted space and it contains at least 30 candies.

Here’s the output from this program:

```
There are 42 candies per candy box
For the standard boxes there are 144 candy boxes per carton
with 648 cubic inches wasted.

CUSTOM CANDY BOX ANALYSIS (No Waste)

Trial Box L = 5 W = 4.5 H = 2
Trial Box contains 30 candies and a carton contains 216 candy boxes.

Trial Box L = 5 W = 4.5 H = 2
Trial Box contains 30 candies and a carton contains 216 candy boxes.

Trial Box L = 6 W = 4.5 H = 2
Trial Box contains 36 candies and a carton contains 180 candy boxes.

Trial Box L = 6 W = 5 H = 2
Trial Box contains 40 candies and a carton contains 162 candy boxes.

Trial Box L = 7.5 W = 3 H = 2
Trial Box contains 30 candies and a carton contains 216 candy boxes.
```

You have a duplicate solution due to the fact that, in the nested loop, you evaluate boxes that have a length of 5 and a width of 4.5, as well as boxes that have a length of 4.5 and a width of 5. Because the CBox class constructor ensures that the length is not less than the width, these two are identical. You could include some additional logic to avoid presenting duplicates, but it hardly seems worth the effort. You could treat it as a small exercise if you like.

# Organizing Your Program Code

In this last example, you distributed the code among several files for the first time. Not only is this common practice with C++ applications generally, but with Windows programming it is essential. The sheer volume of code involved in even the simplest program necessitates dividing it into workable chunks.

As discussed in the previous section, there are basically two kinds of source code file in a C++ program, .h files and .cpp files. This is illustrated in Figure 8-14.

There’s the executable code that corresponds to the definitions of the functions that make up the program. Also, there are definitions of various kinds that are necessary for the executable code to compile correctly. These are global constants and variables, data types that include classes, structures, and unions, and function prototypes. The executable source code is stored in files with the extension .cpp, and the definitions are stored in files with the extension .h.