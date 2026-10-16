```
```cpp
int main()
{
    int i = 11,
        j = 22,
        k = 33;

    int * iPtr = &i;
    int * jPtr = &j;
    int * kPtr = &k;

    cout << "\nAt address " << iPtr
         << ", the value " << *iPtr << " is stored.\n"
         << "\nAt address " << jPtr
         << ", the value " << *jPtr << " is stored.\n"
         << "\nAt address " << kPtr
         << ", the value " << *kPtr << " is stored.\n";
}
```
```

# SAMPLE RUN:

At address 0xbffff970, the value 11 is stored.

At address 0xbffff96c, the value 22 is stored.

At address 0xbffff968, the value 33 is stored.

# 15.1.1 Declaring and Initializing Pointers

We begin with the second set of declarations in the program in Example 15.1:

```
```cpp
int * iPtr = &i;
int * jPtr = &j;
int * kPtr = &k;
```
```

There are two new items in these statements:

+   1. *An asterisk (*) following the type name in a declaration of the form*
+   
+      ```cpp
+      type * variableName;
+      ```
+   
+      declares that `variableName` can store the address of a memory location where a value of the specified `Type` is stored. Such variables are often called **pointer variables**, or simply pointers. Thus, the declarations
+   
+      ```cpp
+      int * iPtr;
+      int * jPtr;
+      int * kPtr;
+      ```