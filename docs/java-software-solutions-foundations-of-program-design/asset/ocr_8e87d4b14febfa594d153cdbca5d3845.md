SR 3.31 By using an enumerated type, you guarantee that variables of that type will only take on the enumerated values.

# 3.8 Wrapper Classes

SR 3.32 A wrapper class is defined in the Java standard class library for each primitive type. In situations where objects are called for, an object created from a wrapper class may suffice.

SR 3.33 The corresponding wrapper classes are Byte, Integer, Double, Character, and Boolean.

SR 3.34 One approach is to use the constructor of Integer, as follows:

```
holdNumber = new Integer(number);
```

Another approach is to take advantage of autoboxing, as follows:

```
holdNumber = number;
```

SR 3.35 The following statement uses the MAX_VALUE constant of the Integer class to print the largest possible int value:

```
System.out.println (Integer.MAX_VALUE);
```

# 3.9 Components and Containers

SR 3.36 Both a frame and a panel are containers that can hold GUI elements. However, a frame is displayed as a separate window with a title bar, whereas a panel cannot be displayed on its own. A panel is often displayed inside a frame.

SR 3.37 The term that best matches is

+   a. container    b. frame    c. panel    d. heavyweight
+   e. lightweight    f. content pane    g. label    h. layout manager

SR 3.38 If you resize the frame by dragging the bottom right corner toward the right, the saying changes from being spread across two lines to being on one line. This happens because no special instructions were included to describe the layout of the container, in which case components of a panel arrange themselves next to each other if the size of the panel allows.

SR 3.39 The best description is “Labels are added to a panel, which is added to a content pane of a frame.”

SR 3.40 The results of the changes are

+   a. Due to the new dimensions the panel is larger and square.