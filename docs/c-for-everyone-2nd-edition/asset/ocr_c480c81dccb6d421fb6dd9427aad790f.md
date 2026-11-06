![](bbox=[0.09, 0.13, 0.15, 0.19])

+   21. Why didn't we initialize the triangular array with the following loop?
+       ```cpp
+       for (int i = 0; i < 10; i++)
+       {
+           counts[i] = new int[i];
+       }
+       ```
+   22. Suppose a program initializes a triangular array as we did in this section, and then accesses a non-existent element with the statement `counts[1][2]++` Will the program compile? If so, what happens at run time?
+   23. Initialize a triangular 10 x 10 array where the first row has length 10 and the last row has length 1.
+   24. What changes would need to be made to the galton.cpp program so that counts is a `vector<int>`?
+   25. What changes would need to be made to the galton.cpp program so that each row is a `vector<int>`?

**Practice It** Now you can try these exercises at the end of the chapter: R7.22, P7.11, P7.12.

# # 7.6 Problem Solving: Draw a Picture

When designing programs that use pointers, you want to visualize how the pointers connect the data that you are working with. In most situations, it is essential that you draw a diagram that shows the connections.

Start with the data that will be accessed or modified through the pointers. These may be account balances, counters, character strings, or other items. Focus on what is being pointed at.

Then draw the variable or variables that contain the pointers. These will be the front-end to your system. Processing usually starts with a pointer, then locates the actual data.

Draw the data that is being processed, then draw the pointer variables. When drawing the pointer arrows, illustrate a typical situation.

Finally, draw the pointers as arrows. If the pointers will vary as the program executes, draw a typical arrangement. It can also be useful to draw several diagrams that show how the pointers change.

Consider the following problem: The media center of a university loans out equipment, such as microphones, cables, and so on, to faculty and students. We want to track the name of each item, and the name of the user who checked it out.

In this case, the data that are being accessed are item and user names. We will store all names in a long array of characters, adding new names to the end as needed. If a name is already present, we don't store it twice. This is an efficient way of storing strings, provided that few strings need to be removed. Here is a section of the character array:

```
Microphone TX-10\0 Smith, Diane\0 Lee, Tim\0 Tape recorder\0 Mini PVI cable\0 ...
```

Next, let us draw the pointers to the item names. they are stored in an array of pointers called items. Some items may have the same name. In the example below, we have two microphones with the same name.