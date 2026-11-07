# Problems with C Strings

Although C strings provide a way to use strings, they are more error prone and not as robust as C++ strings. We therefore recommend C++ strings be used as much as possible. We discuss C++ strings in the next section.

# 10.2 THE C++ STRING CLASS

The C++ library provides a class named *string*, whose objects are normally referred to as C++ string objects as compared to C string arrays of characters. To use the objects and member functions of this class, we must include the header file `<string>` in our program.

The C++ string library defines a class type whereas the C string library defines an array of characters. When working with a C string, we must create an array of characters and apply functions defined in the <cstring> library. When using a C++ string, we can construct a string object and apply the predefined member functions in the <string> library to it. We strongly recommend using the C++ string as much as possible.

> To use C++ strings, we need the `<string>` header file.

# 10.2.1 General Design Idea

To better understand how the string class works, we must consider general concepts that designers use in designing the string class. The string class has private data members and public member functions. The user calls the public member functions to manipulate string objects. In general, the data members include a pointer to an array of characters. Other data members keep information about the character array. The data members are normally created in stack memory, but the character array itself is allocated in the heap because its size is not defined until run time. While the C++ string can be visualized as a character array, it is not null terminated as we saw in C strings. Figure 10.7 shows the general picture of a C++ string.

> A C++ string is an array of characters, but it is not null terminated.

![](bbox=[0.3, 0.695, 0.759, 0.862])

+   **Notes:**
+   1. A C++ string is not null terminated.
+   2. Size must be less than or equal to capacity.
+   3. The front is at index 0.
+   4. The back is at index (size − 1).

Figure 10.7  General idea behind the C++ string object