```
```cpp
12    char *ptr2 = new char[ length + 1 ]; // including null
14    // copy characters from string1 into allocated memory
15    string1.copy( ptr2, length, 0 ); // copy string1 to ptr2 char*
16    ptr2[ length ] = '\0'; // add null terminator
18    cout << "string string1 is " << string1
19          << "\nstring converted to a C-Style string is "
20          << string1.c_str() << "\nptr1 is";
22    // Assign to pointer ptr1 the const char * returned by
23    // function data(). NOTE: this is potentially dangerous
24    // assignment. If string1 is modified, pointer ptr1 can
25    // become invalid.
26    ptr1 = string1.data();
28    // output each character using pointer
29    for ( int i = 0; i < length; ++i )
30        cout << *( ptr1 + i ); // use pointer arithmetic
32    cout << "\nptr2 is " << ptr2 << endl;
33    delete [] ptr2; // reclaim dynamically allocated memory
34  } // end main
```
```

```
```text
string string1 is STRINGS
string converted to a C-Style string is STRINGS
ptr1 is STRINGS
ptr2 is STRINGS
```
```

**Fig. 18.9** | *Converting strings to C-style strings and character arrays. (Part 2 of 2.)*

The program declares a string, an int and two char pointers (lines 9–12). The string string1 is initialized to "STRINGS", ptr1 is initialized to 0 and length is initialized to the length of string1. Memory of sufficient size to hold a pointer-based string equivalent of string string1 is allocated dynamically and attached to char pointer ptr2.

Line 15 uses string member function copy to copy object string1 into the char array pointed to by ptr2. Line 16 manually places a terminating null character in the array pointed to by ptr2.

Line 20 uses function c_str to obtain a const char * that points to a null terminated C-style string with the same content as string1. The pointer is passed to the stream insertion operator for output.

Line 26 assigns the const char * ptr1 a pointer returned by class string member function data. This member function returns a non-null-terminated C-style character array. We do not modify string1 in the example. If string1 were to be modified (e.g., the string’s dynamic memory changes its address due to a member function call such as string1.insert( 0, "abcd" );), ptr1 could become invalid—which could lead to unpredictable results.

Lines 29–30 use pointer arithmetic to output the character array pointed to by ptr1. In lines 32–33, the C-style string pointed to by ptr2 is output and the memory allocated for ptr2 is deleted to avoid a memory leak.