To declare a pointer variable, you need to specify the type of variable it will point to. Then you precede the variable’s name with an asterisk, as in the following:

```
int *ptr;
```

This line declares a variable that *points* to an integer. In other words, it can contain *the address* of an integer variable. And how do you grab the address of an integer variable? Easy! By using the `&` notation! Thus, you can do something like this:

```
ptr = &NumberOfPotholes;
```

This line puts the address of the variable `NumberOfPotholes` in the `ptr` variable. Remember that `ptr` doesn’t hold the number of potholes; rather, it holds the address of the variable called `NumberOfPotholes`.

![](bbox=[0.163, 0.365, 0.226, 0.432])

You specify the type of pointer by the type of item it points to. If a pointer variable points to an integer, its type is *pointer to integer*. In C++ notation, its type is `int *` (with a space between them) or `int*` (no space); you are allowed to enter it with or without a space. If a pointer variable points to a string, its type is *pointer to string*, and notation for this type is `string *`.

![](bbox=[0.163, 0.464, 0.226, 0.531])

The `ptr` variable holds an address, but what’s at that address? That address is the location in memory of the storage bin known as `NumberOfPotholes`. Right at that spot in memory is the data stored in `NumberOfPotholes`.

![](bbox=[0.163, 0.546, 0.226, 0.613])

Think this pointer concept through carefully. If you have to, reread this section a few times until it’s locked in your head. Then meditate on it. Wake up in the night thinking about it. Call strangers on the telephone and chitchat about it. The more you understand pointers, the better off your programming career will be — and the more likely you are to make a million dollars.

# Changing a variable by using a pointer

After you have a pointer variable holding another variable’s address, you can use the pointer to access the information in the other variable. That means you have two ways to get to the information in a variable: Use the variable name itself (such as `NumberOfPotholes`), or use the pointer variable that points to it.

If you want to store the number 6087 in `NumberOfPotholes`, you can do this:

```
NumberOfPotholes = 6087;
```