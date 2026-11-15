# 6.17 Handling arrays

# 6.17.1 Introduction

Array handling is greatly simplified in EMBOSS. AJAX provides dynamic array objects which grow automatically as required thereby saving you the bother of managing the memory yourself. This makes your code cleaner and less error-prone. Objects are provided for handling arrays of various dimensions (1D, 2D or 3D) of the following C datatypes:

+   - Character (char)
+   - Short integer (ajshort)
+   - Unsigned integer (ajuint)
+   - Integer (ajint)
+   - Floating point number (float)
+   - Long floating point number (ajlong)
+   - Double-precision floating point number (double).

The objects can be allocated to a default or a specified reserved size. Each object keeps track of the reserved space available (in case a function is called which must extend the array) and the actual length of the array. Arrays of higher dimensions can nest arrays of lower dimensions.

Functions are provided for returning the current length and for getting and setting array elements. The array elements should only ever be accessed using these functions. If you assign a value to an element which is beyond the current size of the array, then the array will be dynamically reallocated to a sufficient size to accommodate the new element. In contrast, if you try to retrieve an element beyond the current size of the array an error will be generated.

The C-type array may be retrieved from any of the array objects should this be required. This allows standard array notation to be used to access array elements. Functions are provided to sort C-type arrays of integers, unsigned integers and floating point numbers in various ways.

Array objects are typically created directly within the C source code. A floating point array can however be specified in the ACD file (the array ACD datatype) and a pointer to a corresponding AJAX object (AjPFloat) retrieved by the program.

# 6.17.2 AJAX library files

AJAX library files for handling arrays are listed in the table below. Library file documentation, including a complete description of datatypes and functions, is available at: http://emboss.open-bio.org/rel/dev/libs/

| Library file documentation | Description |
|---|---|
| ajarr | General array handling |
| ajsort | Array sorting |