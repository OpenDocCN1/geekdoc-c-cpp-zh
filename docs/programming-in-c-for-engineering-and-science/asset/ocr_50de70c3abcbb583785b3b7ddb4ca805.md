Although these operations suffice to solve the problem at hand, designing a reusable and useful class involves identifying other operations that a user of the class is likely to need. To that end, we might extend our list with the following operations:

+   vii. Construct myself *explicitly* by initializing my degrees and scale members with specified values.
+   viii. Report my number of degrees.
+   ix. Report my scale.
+   x. Compute my temperature raised by a given number of degrees.
+   xi. Compute my temperature lowered by a given number of degrees.
+   xii. Compare myself to another `Temperature` object using any of the six relational operators (==, !=, <, >, <=, >=).
+   xiii. Assign another `Temperature` value to me using the assignment operator (=).

This is not an exhaustive list, but it is a good start and will serve to introduce the details of class implementation. Other operations can be added later.

The last operation, assignment, is already provided. For any class we define, the C++ compiler creates a *default assignment operation* that is adequate for our purposes. Thus, a statement like

```
temp2 = temp1;
```

can be used to copy the data members of temp1 into temp2. We must implement the other operations ourselves as described in the next section.

# 14.2.3 Temperature Class's Data

To identify what data will be needed for a class, it is a good idea to begin by going through the list of operations and identifying what information each of them requires. For our Temperature class, operations (i) and (vi–xi) indicate that, from an internal perspective, the following are needed:

+   1. My degrees, and
+   2. My scale

In fact, these are the only data items that are needed for our Temperature class. For other classes, however, a complete list may not be evident at the outset and others will have to be added later when the implementation of an operation requires them.

# 14.3 IMPLEMENTING A CLASS

Once we have a design for a class, we can use it as a blueprint for implementing the class. Because we want the class to be reusable, it is declared in a library's header file (e.g.,