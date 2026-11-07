Program 6.15 Using a swap function (Continued)

```
```cpp
// Declaration
int first = 10;
int second = 20;
swap (first, second); // Function call

// Printing to test swapping
cout << "Value of first in main: " << first << endl;
cout << "Value of second in main: " << second << endl;
return 0;
}
/****************************************************************
 * The swap function takes two parameters as pass-by-reference. *
 * It then swaps the values of fst and snd using a temporary    *
 * variable named temp. Since the data are passed by reference, *
 * changing the parameters in the swap means changing values in *
 * the arguments (first and second in main).                    *
 ****************************************************************/
void swap (int& fst, int& snd)
{
  int temp = fst;
  fst = snd;
  snd = temp;
  return;
}
```
```

```
```text
Run:
Value of first in main: 20
Value of second in main: 10
```
```

# Pass-by-Pointer

In the **pass-by-pointer** mechanism, the argument sends a memory address to the corresponding parameter. The parameter stores the address and can access the value stored in the argument through that address. The pass-by-pointer mechanism is used in the C language because pass-by-reference does not exist in C. It is still used to some extent in C++. We discuss pass-by-pointer after we discuss pointers in Chapter 9.

# Advantages and Disadvantages

Before closing this section, we briefly review the advantages and disadvantages of each method.

+   a. Pass-by-value is very simple and protects arguments from being changed by the called function. However, it has one disadvantage: The argument object needs to be copied and passed from the calling function to the called function. If the object is small, like the built-in data types we have used so far, copying is not expensive and we should use this method. We will see in Chapter 9, however, that we do not use pass-by-value in object-oriented programming when the object size is large. We use the other methods (pass-by-reference and pass-by-pointer).