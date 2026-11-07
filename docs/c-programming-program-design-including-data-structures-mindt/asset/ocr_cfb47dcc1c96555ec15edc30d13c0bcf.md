```
```text
if average is greater than or equal to 60
    grade = D
otherwise
    grade = F
```
```

You can use the solutions to these subproblems to design the main algorithm as follows:\n(Suppose **totalAverage** stands for the sum of the averages of each student's test average.)

+   1. **totalAverage = 0;**\n2. *Repeat* the following steps for each student in the class:\n   a. Get student's name.\n   b. Use the algorithm as discussed above to find the average test score.\n   c. Use the algorithm as discussed above to find the grade.\n3. Update **totalAverage** by adding the current student's average test score.\n4. Determine the class average as follows:\n   **classAverage = totalAverage / 10**

A programming exercise in Chapter 8 asks you to write a C++ program to calculate the average test score and grade for each student in a class.

> **NOTE**\n\nEarlier in this chapter, we described the problem analysis, coding, and execution cycle. In this section, we gave various examples to illustrate the problem analysis and coding cycle. It must be pointed out that problem analysis is the most important part of programming. Once you have analyzed the problem and written the necessary steps of the solution in your native language, then, as you will see throughout the text, writing the C++ code to implement your solution is relatively easy. In addition, soon you will recognize that the steps of your solutions can be effectively stated into a C++ code. Furthermore, a good problem analysis will lead to a better and cleaner program. Even though we have not yet introduced the syntax of C++, to illustrate how to write a C++ code corresponding to the steps of your solution, let us consider the algorithm designed in Example 1-1. Suppose *length*, *width*, *perimeter*, and *area* represents the length, width, perimeter, and area of a rectangle. Here are the four steps of the algorithm and their corresponding C++ statement:

| Algorithm Step | C++ Instruction (Code) |
|---|---|
| 1. Get the length of the rectangle. | `cin >> length;` |
| 2. Get the width of the rectangle. | `cin >> width;` |
| 3. Calculate the perimeter. | `perimeter = 2 * (length + width);` |
| 4. Calculate the area. | `area = length * width;` |

Consider the first statement. In C++, `cin` stands for common input. During program execution, the code associated with it instructs the user to input data and if the user enters a valid datum, then that datum will be stored in the memory, that is, the memory becomes the value.