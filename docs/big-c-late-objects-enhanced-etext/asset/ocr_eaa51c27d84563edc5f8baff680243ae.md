# CHAPTER SUMMARY

# Define and use pointer variables.

+   - A pointer denotes the location of a variable in memory.
+   - The type T* denotes a pointer to a variable of type T.
+   - The & operator yields the location of a variable.
+   - The * operator accesses the variable to which a pointer points.
+   - It is an error to use an uninitialized pointer.
+   - The nullPtr pointer does not point to any object.

![](bbox=[0.78, 0.2, 0.95, 0.33])

# Understand the relationship between arrays and pointers in C++.

+   - The name of an array variable is a pointer to the starting element of the array.
+   - Pointer arithmetic means adding an integer offset to an array pointer, yielding a pointer that skips past the given number of elements.
+   - The array/pointer duality law states that a[n] is identical to *(a + n), where a is a pointer into an array and n is an integer offset.
+   - When passing an array to a function, only the starting address is passed.

# Use C++ string objects with functions that process character arrays.

+   - A value of type char denotes an individual character. Character literals are enclosed in single quotes.
+   - A literal string (enclosed in double quotes) is an array of char values with a zero terminator.
+   - Many library functions use pointers of type char*.
+   - The c_str member function yields a char* pointer from a string object.
+   - You can initialize C++ string variables with C strings.
+   - You can access characters in a C++ string object with the [] operator.

![](bbox=[0.75, 0.58, 0.95, 0.66])

![](bbox=[0.48, 0.7, 0.95, 0.82])

# Allocate and deallocate memory in programs whose memory requirements aren't known until run time.

+   - Use dynamic memory allocation if you do not know in advance how many values you need.
+   - The new operator allocates memory from the free store.
+   - You must reclaim dynamically allocated objects with the delete or delete[] operator.
+   - Using a dangling pointer (a pointer that points to memory that has been deleted) is a serious programming error.
+   - Every call to new should have a matching call to delete.

![](bbox=[0.8, 0.82, 0.95, 0.92])