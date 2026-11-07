g) `cout << "The address stored in fPtr is: " << fPtr << endl;`  
Yes, the value is the same.

# 8.5

+   a) `void exchange( double *x, double *y )`  
+   b) `void exchange( double &x, double &y )`  
+   c) `char vowel[] = "AEIOU";`  
+      `char vowel[] = { 'A', 'E', 'I', 'O', 'U', '\0' };`

# 8.6

+   a) *Error:* zPtr has not been initialized.  
+      *Correction:* Initialize zPtr with `zPtr = z;`  
+   
+   b) *Error:* The pointer is not dereferenced.  
+      *Correction:* Change the statement to `number = *zPtr;`  
+   
+   c) *Error:* `zPtr[2]` is not a pointer and should not be dereferenced.  
+      *Correction:* Change `*zPtr[2]` to `zPtr[2]`.  
+   
+   d) *Error:* Referring to a built-in array element outside the built-in array’s bounds with pointer subscript.  
+      *Correction:* To prevent this, change the relational operator in the for statement to `<` or change the 5 to a 4.  
+   
+   e) *Error:* Dereferencing a void pointer.  
+      *Correction:* To dereference the void pointer, it must first be cast to an integer pointer. Change the statement to `number = *static_cast<int *>(zPtr);`  
+   
+   f) *Error:* Trying to modify a built-in array’s name with pointer arithmetic.  
+      *Correction:* Use a pointer variable instead of the built-in array’s name to accomplish pointer arithmetic, or subscribe the built-in array’s name to refer to a specific element.

# Exercises

+   8.7  *(True or False)* State whether the following are true or false. If false, explain why.  
+   a) Two pointers that point to different built-in arrays cannot be compared meaningfully.  
+   b) Because the name of a built-in array is implicitly convertible to a pointer to the first element of the built-in array, built-in array names can be manipulated in the same manner as pointers.

+   8.8  *(Write C++ Statements)* For each of the following, write C++ statements that perform the specified task. Assume that unsigned integers are stored in two bytes and that the starting address of the built-in array is location 1002500 in memory.  
+   
+   a) Declare a built-in array of type `unsigned int` called `values` with five elements, and initialize the elements to the even integers from 2 to 10. Assume that the constant SIZE has been defined as 5.  
+   
+   b) Declare a pointer `vPtr` that points to an object of type `unsigned int`.  
+   
+   c) Use a `for` statement to display the elements of built-in array `values` using array-subscript notation.  
+   
+   d) Write two separate statements that assign the starting address of built-in array `values` to pointer variable `vPtr`.  
+   
+   e) Use a `for` statement to display the elements of built-in array `values` using pointer/offset notation.  
+   
+   f) Use a `for` statement to display the elements of built-in array `values` using pointer/offset notation with the built-in array’s name as the pointer.  
+   
+   g) Use a `for` statement to display the elements of built-in array `values` by subscripting the pointer to the built-in array.  
+   
+   h) Refer to the fifth element of `values` using array subscript notation, pointer/offset notation with the built-in array’s name as the pointer, pointer subscript notation and pointer/offset notation.