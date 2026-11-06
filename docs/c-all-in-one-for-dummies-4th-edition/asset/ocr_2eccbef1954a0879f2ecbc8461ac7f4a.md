```
```cpp
cout << MyPen->InkColor << endl;
delete MyPen;
MyPen = 0;
return 0;
}
```
```

![](bbox=[0.173, 0.222, 0.24, 0.289])

Table 1–2 reiterates the process (steps) shown in Listing 1–6 in a more formal way. The table is called “Steps to Using Objects” rather than something more specific such as “Using Objects with Pointers” because the majority of your work with objects will be through pointers. Therefore, this is the most common way of using pointers.

**TABLE 1-2 — Steps to Using Objects**

| Step | Sample Code | Action |
|---|---|---|
| 1 | `Pen *MyPen;` | Declares the pointer |
| 2 | `MyPen = new Pen;` | Calls new to create the object |
| 3 | `MyPen->InkColor = red;` | Accesses the members of the object through the pointer |
| 4 | `delete MyPen;` | Deletes the object |
| 5 | `MyPen = 0;` | Clears the pointer |

Now that you have an overview of the process through Listing 1–6 and understand the basics through Table 1–2, you can see how to formalize the procedure. The following steps describe precisely how to work with raw pointers and objects:

+   1. **Declare the pointer.** The pointer must match the type of object you intend to work with, except that the pointer’s type name in C++ is followed by an asterisk, `*`.
+   2. **Call `new`, passing the class name, and store the results of `new` in the pointer.** You can combine Steps 1 and 2 into a single step.
+   3. **Access the object’s members through the pointer with the arrow operator, `->`.** You could dereference the pointer and put parentheses around it, but everyone uses the shorthand notation.