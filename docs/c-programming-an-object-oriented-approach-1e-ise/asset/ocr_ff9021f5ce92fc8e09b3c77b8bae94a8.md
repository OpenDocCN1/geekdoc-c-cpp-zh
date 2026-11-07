The string *str1* is made of the same five characters (the *size_type* here defines the length). The string *str2* is made of a string literal. In this case, the function copies all characters in the literal (except the null character at the end) to the string object. The string *str3* is part of a string literal. If we want to use a part of the C-string object (here and later in other member functions), we must start at the beginning of the string because the pointer to a string literal is a constant pointer and cannot be moved. However, we can define the number of characters that should be copied. In this case, we have said we want only two characters, which means only "he" is used to create a C++ string object.

# ### Destruction

The destructor of the string class simply deletes the character array created in the heap and pops all data members allocated in the stack. In other words, calling the delete operator to free allocated memory is done by the destructor, which helps prevent memory leaks.

# ### Copy Construction

The string class allows us to use two different copy constructors: a copy constructor comprised of a full existing object or a copy constructor comprised of part of an existing object.

```
```cpp
string str (oldStr);                  // Using the whole oldStr
string str (oldStrg, index, length);  // Using part of the oldStr
```
```

# ### Size and Capacity

A C++ string object uses an array of characters in the heap. If the size of the array must be decreased during an operation, the value of the *size* member function is changed. However, if the size of the string must be increased during an operation, reallocation is needed. A bigger array must be created in the heap, the value of the existing elements must be copied, the new elements must be filled, and the original memory recycled. This is done by the private member functions in the background. However, this process can create a huge overhead for the system if many small incremental changes in the size are needed. To prevent this overhead, the system allows the user to make a reservation, which leads to a larger array than needed when the array is created.

**Size and Maximum Size** There are two functions that return values of the string size. The *size* function returns the number of characters currently in the string object. The *max_size* function returns the maximum number of characters that a string object can have; it is normally a very big number that is system dependent.

```
```cpp
size_type n = strg.size();        // Getting the size
size_type n = strg.max_size();    // Getting the maximum size
```
```

**Resizing** The *resize* function changes the size of the string. If *n* < *size*, characters are deleted from the end of the string to make the size equal to *n*; if *n* > *size*, copies of character *c* are added to the end of the string to make the size *n*.

```
```cpp
strg.resize (n, 'c');             // Resizing and filling the rest of string with 'c'
```
```