the last element is stored in the last reserved location. This contiguous storage allocation is a key feature of arrays because it provides a simple mechanism for locating any element in the list easily.

Because elements in the array are stored sequentially, any single element can be accessed by giving the array’s name and the element’s position. This position is called the element’s **index** or **subscript** value. (The two terms are synonymous.) For a one-dimensional array, the first element has an index of 0, the second element has an index of 1, and so on. In C++, the array name and element index are combined by listing the index in braces after the array name. For example, the declaration `double grade[5];` creates five elements, with the following correspondences:

+   `grade[0]` refers to the first grade stored in the grade array  
+   `grade[1]` refers to the second grade stored in the grade array  
+   `grade[2]` refers to the third grade stored in the grade array  
+   `grade[3]` refers to the fourth grade stored in the grade array  
+   `grade[4]` refers to the fifth grade stored in the grade array

Figure 7.2 shows the grade array in memory with the correct designation for each array element. Each element is referred to as an **indexed variable** or a **subscripted variable** because both a variable name (the array name, in this case) and an index or a subscript value must be used to reference the element. Remember that the index or subscript value gives the element’s position in the array.

![](bbox=[0.257, 0.527, 0.813, 0.605])

**Figure 7.2**  Identifying array elements

The subscripted variable, `grade[0]`, is read as “grade sub zero” or “grade zero.” It’s a shortened way of saying “the grade array subscripted by zero.” Similarly, `grade[1]` is read as “grade sub one” or “grade one,” `grade[2]` as “grade sub two” or “grade two,” and so on.

Although referencing the first element with an index of 0 might seem unusual, doing so increases the computer’s speed when it accesses array elements. Internally, unseen by the programmer, the computer uses the index as an offset from the array’s starting position. As shown in Figure 7.3, the index tells the computer how many elements to skip, starting from the beginning of the array, to get to the correct element.