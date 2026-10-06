# Figure 8-14 The names and addresses arrays

| names[0] | names[1] | names[2] | names[3] | names[4] |
| --- | --- | --- | --- | --- |
| Person #1 | Person #2 | Person #3 | Person #4 | Person #5 |
| addresses [0] | addresses [1] | addresses [2] | addresses [3] | addresses [4] |

The names and addresses arrays are examples of parallel arrays. Parallel arrays are two or more arrays that hold related data, and the related elements in each array are accessed with a common subscript.

# In the Spotlight:
Using Parallel Arrays

In this chapter's first In the Spotlight section (see Program 8-4), Megan asked you to design a program that allows her to enter the number of hours worked by each employee and displays each employee's gross pay. As it is currently designed, the program refers to employees as "employee 1", employee 2," and so on. Megan asked you to modify the program so she can enter employees' names along with their hours, and it should display each employee's name with or her gross pay.

Currently, the program has an array hours that holds each employee's hours worked. You decide to add a parallel array named names that will hold each employee's name. The first employee's data will appear in names[0] and in hours[0], the second employee's data will appear in names[1] and in hours[1], and so on.

Here is the updated algorithm:

+   1. For each employee:
   a. Get the employee's name and store it in the names array.
   b. Get the employee's number of hours worked and store it in the corresponding element of the hours array.
2. Step through each set of elements in the parallel arrays and display the employee's name and gross pay.

Program 8-15 shows the pseudocode for the revised program, and Figure 8-15 shows a flowchart.