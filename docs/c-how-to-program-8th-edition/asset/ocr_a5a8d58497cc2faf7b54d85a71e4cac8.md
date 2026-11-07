+   - A static local variable in a function definition exists for the duration of the program but is visible only in the function body.
+   - A program initializes static local arrays when their declarations are first encountered. If a static array is not initialized explicitly by you, each element of that array is initialized to zero by the compiler when the array is created.

# Section 7.5 Passing Arrays to Functions

+   - To pass an array argument to a function, specify the name of the array without any brackets. To pass an element of an array to a function, use the subscripted name of the array element as an argument in the function call.
+   - Arrays are passed to functions by reference—the called functions can modify the element values in the callers’ original arrays. The value of the name of the array is the address in the computer’s memory of the first element of the array. Because the starting address of the array is passed, the called function knows precisely where the array is stored in memory.
+   - Individual array elements are passed by value exactly as simple variables are.
+   - To receive an array argument, a function’s parameter list must specify that the function expects to receive an array. The size of the array is not required between the array brackets.
+   - The type qualifier const (p. 273) can be used to prevent modification of array values in the caller by code in a called function. When an array parameter is preceded by the const qualifier, the elements of the array become constant in the function body, and any attempt to modify an element of the array in the function body results in a compilation error.

# Section 7.6 Case Study: Class Gradebook Using an Array to Store Grades

+   - Class variables (static data members; p. 290) are shared by all objects of the class in which the variables are declared.
+   - A static data member can be accessed within the class definition and the member-function definitions like any other data member.
+   - A public static data member can also be accessed outside of the class, even when no objects of the class exist, using the class name followed by the scope resolution operator (::) and the name of the data member.

# Section 7.7 Searching Arrays with Linear Search

+   - The linear search (p. 293) compares each array element with a search key (p. 293). Because the array is not in any particular order, it’s just as likely that the value will be found in the first element as the last. On average, a program must compare the search key with half the array elements. To determine that a value is not in the array, the program must compare the search key to every element in the array.

# Section 7.8 Sorting Arrays with Insertion Sort

+   - An array can be sorted using insertion sort (p. 295). The first iteration of this algorithm takes the second element and, if it’s less than the first element, swaps it with the first element (i.e., the program inserts the second element in front of the first element). The second iteration looks at the third element and inserts it into the correct position with respect to the first two elements, so all three elements are in order. At the iᵗʰ iteration of this algorithm, the first i elements in the original array will be sorted. For small arrays, the insertion sort is acceptable, but for larger arrays it’s inefficient compared to other more sophisticated sorting algorithms.

# Section 7.9 Multidimensional Arrays

+   - Multidimensional arrays (p. 297) with two dimensions are often used to represent tables of values (p. 297) consisting of information arranged in rows and columns.