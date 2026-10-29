# How to Use a Dynamic Array

+   - Define a pointer type: Define a type for pointers to variables of the same type as the elements of the array. For example, if the dynamic array is an array of doubles, you might use the following:
+   
+   ```
+   typedef double* DoubleArrayPtr;
+   ```
+   - Declare a pointer variable: Declare a pointer variable of this defined type. The pointer variable will point to the dynamically allocated array in memory and will serve as the name of the dynamic array.
+   
+   ```
+   DoubleArrayPtr a;
+   ```
+   (Alternatively, without a defined pointer type, use double *a;).
+   - Call new: Create a dynamic array using the new operator:
+   
+   ```
+   a = new double[arraySize];
+   ```
+   The size of the dynamic array is given in square brackets as in the above example. The size can be given using an int variable or other int expression. In the above example, arraySize can be a variable of type int whose value is determined while the program is running.
+   - Use like an ordinary array: The pointer variable, such as a, is used just like an ordinary array. For example, the indexed variables are written in the usual way: a[0], a[1], and so forth. The pointer variable should not have any other pointer value assigned to it, but should be used like an array variable.
+   - Call delete []: When your program is finished with the dynamically allocated array variable, use delete and empty square brackets along with the pointer variable to eliminate the dynamic array and return the storage that it occupies to the freestore manager for reuse. For example:
+   
+   ```
+   delete [] a;
+   ```

The resulting array m is a three-by-four dynamic array. A simple program to illustrate this is given in Display 10.9.

Be sure to notice the use of delete in Display 10.9. Since the dynamic array m is an array of arrays, each of the arrays created with new in the for loop on lines 13 and 14 must be returned to the freestore manager with a call to delete []; then, the array m itself must be returned to the freestore manager with another call to delete []. There must be a call to delete [] for each call to new that created an array. (Since the program ends right after the calls to delete [], we could safely omit the calls to delete [], but we wanted to illustrate their usage.)