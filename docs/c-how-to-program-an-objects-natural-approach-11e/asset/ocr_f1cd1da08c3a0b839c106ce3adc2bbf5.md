We’ve added a similar capability to the MyArray class. Line 111 displays `ints4`’s current contents, then line 112 uses `++ints4` to preincrement the MyArray, adding one to each element. This expression’s result is the updated MyArray. We then use MyArray’s overloaded **stream insertion operator** (`<<`) to display the contents.

```
```cpp
// add one to every element of ints4 using preincrement
std::cout << "\nints4: " << ints4;
std::cout << "\npreincrementing ints4: " << ++ints4;
```
```

```
```text
ints4: {10, 20, 30}
preincrementing ints4: {11, 21, 31}
```
```

# Postincrementing Every ints4 Element with the Overloaded ++ Operator

Line 115 postincrements the entire MyArray with the expression `ints4++`. Recall that a postincrement returns its operand’s **previous value**, as confirmed by the program’s output. The postincrement operator’s implementation, which we’ll discuss in Section 11.6.14, produces the outputs showing that MyArray’s **copy constructor** and **destructor** were called.

```
```cpp
// add one to every element of ints4 using postincrement
std::cout << "\npostincrementing ints4: " << ints4++ << "\n";
std::cout << "\nints4 now contains: " << ints4;
```
```

```
```text
postincrementing ints4: MyArray copy constructor
{11, 21, 31}
MyArray destructor

ints4 now contains: {12, 22, 32}
```
```

# Adding a Value to Every ints4 Element with the Overloaded += Operator

Class MyArray also provides a **broadcasting assignment overloaded addition** operator (`+=`) for adding an int value to every MyArray element. Line 119 adds 7 to every ints4 element, then displays its new contents. Note that the non-overloaded versions of `++` and `+=` still work on individual MyArray elements, too—those are simply int values.

```
```cpp
// add a value to every element of ints4 using +=
std::cout << "\nAdd 7 to every ints4 element: " << (ints4 += 7)
          << "\n";
}
```

```
```text
Add 7 to every ints4 element: {19, 29, 39}
```
```

# Destroying the MyArray Objects That Remain

When main terminates, the destructors are called for the five MyArray objects created in main, producing the last five lines of the program’s output.