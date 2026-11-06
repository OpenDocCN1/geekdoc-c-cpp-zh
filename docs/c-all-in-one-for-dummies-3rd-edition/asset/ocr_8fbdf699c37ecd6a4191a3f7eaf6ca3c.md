![](bbox=[0.238, 0.13, 0.853, 0.504])

Figure 5-5: Using the Filesystem library requires the System library as well.

Book VI Chapter 5

Boosting a Step

![](bbox=[0.057, 0.495, 0.152, 0.569])

# ## The Filesystem library and the Standard library

The developers of the Boost library continuously add to its capabilities. Some of the additions developers make are so useful that they end up in the Standard library. The Filesystem library is one of these useful elements. You can see the proposal for adding the Filesystem library to the Standard library at http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2006/n1975.html.

Of course, standardized libraries require discussion from multiple groups, not just the Boost developers. Consequently, the Boost library you use today may not be precisely the same library you see added to the Standard library. It's important to keep up with the proposed technical changes to the Boost library as they move to the Standard library by reviewing the documentation online.

The Boost library documentation appears at http://www.boost.org/doc/libs/1_55_0/?view=categorized.

The movement of code from one setting to another tends to confuse developers because they suddenly find that a favorite library has seemingly disappeared. These developers also question whether they should continue using the old library or move to the new one. In all cases, you want to use the Standard library when you can because the Standard library is fully supported by a standards group, and well, standard. Consequently, when the Filesystem library finally makes the move to the Standard library, be prepared to make a change in how you work with it and update your code as needed to ensure full compliance with the code everyone else creates.