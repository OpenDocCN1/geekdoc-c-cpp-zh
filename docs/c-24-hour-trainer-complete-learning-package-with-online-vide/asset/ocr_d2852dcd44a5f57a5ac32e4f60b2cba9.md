# TRY IT

In this Try It, you build a program that prints and displays a preview of the table shown in Figure 30-7. You build an array of student objects and then loop through them, displaying their values as shown in the figure.

![](bbox=[0.13, 0.26, 0.9, 0.55])

| Name | Test 1 | Test 2 | Test 3 | Test 4 |
|---|---|---|---|---|
| Ann Archer | 91 | 92 | 93 | 94 |
| Bob Blarth | 81 | 82 | 83 | 84 |
| Cyd Carter | 71 | 72 | 73 | 74 |
| Dan Deever | 61 | 62 | 63 | 64 |

FIGURE 30-7

# Lesson Requirements

In this lesson, you:

+   - Start a new Windows Forms project and create the program's main form. Add PrintDocument and PrintPreviewDialog components to do the printing and previewing.
+   - Add Print and Preview buttons with appropriate event handlers.
+   - Add a Student class with FirstName and LastName properties. Also give it a TestScores property that is an array of integers
+   - Create the PrintPage event handler.
+     - Create an array of Student objects. Initialize them using array and object initializers.
+     - Loop through the Student objects, printing them.
+     - Draw a rectangle around the table.

> NOTE You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

# Hints

+   - Don't forget to set the PrintPreviewDialog's Document property, to the PrintDocument component.
+   - This example doesn't do anything fancy with Student properties, so they can be auto-implemented.