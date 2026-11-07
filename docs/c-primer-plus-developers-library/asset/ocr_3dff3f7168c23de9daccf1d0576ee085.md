You use the new `[]` operator to create an array with dynamic binding (a dynamic array)—that is, an array that is allocated and whose size can be set during runtime. You free the memory with `delete []` when you are done:

```
int size;
cin >> size;
int * pz = new int [size];  // dynamic binding, size set at run time
...
delete [] pz;               // free memory when finished
```

# Array Notation and Pointer Notation

Using bracket array notation is equivalent to dereferencing a pointer:

```
tacos[0] means *tacos means the value at address tacos
tacos[3] means *(tacos + 3) means the value at address tacos + 3
```

This is true for both array names and pointer variables, so you can use either pointer notation or array notation with pointers and array names.

Here are some examples:

```
int * pt = new int [10];  // pt points to block of 10 ints
*pt = 5;                  // set element number 0 to 5
pt[0] = 6;                // reset element number 0 to 6
pt[9] = 44;               // set tenth element (element number 9) to 44
int coats[10];
*(coats + 4) = 12;         // set coats[4] to 12
```

# Pointers and Strings

The special relationship between arrays and pointers extends to C-style strings. Consider the following code:

```
char flower[10] = "rose";
cout << flower << " is a red\n";
```

The name of an array is the address of its first element, so flower in the cout statement is the address of the char element containing the character r. The cout object assumes that the address of a char is the address of a string, so it prints the character at that address and then continues printing characters until it runs into the null character (\0). In short, if you give cout the address of a character, it prints everything from that character to the first null character that follows it.

The crucial element here is not that flower is an array name but that flower acts as the address of a char. This implies that you can use a pointer-to-char variable as an argument to cout also because it, too, is the address of a char. Of course, that pointer should point to the beginning of a string. We’ll check that out in a moment.

But what about the final part of the preceding cout statement? If flower is actually the address of the first character of a string, what is the expression " is a red\n"? To be consistent with cout’s handling of string output, this quoted string should also be an