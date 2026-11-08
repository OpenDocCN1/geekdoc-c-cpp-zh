# Hexadecimal Memory Addresses

![](bbox=[0.169, 0.2, 0.786, 0.456])

As you know, an integer has a different representation from a floating-point value, and the number of bytes occupied by an item of data depends on what it is. So, to use a data item stored at the address contained in a pointer, you need to know the type of the data. If a pointer were nothing more than the address of some arbitrary data, it would not be all that interesting. Without knowing the type of data, a pointer is not of much use. Each pointer therefore points to a particular type of data item at that address. This will become clearer when we get down to specifics, so let's look at how to define a pointer. The definition of a pointer is similar to that of an ordinary variable except that the type name has an asterisk following it to indicate that it's a pointer and not a variable of that type. Here's how you define a pointer called pnumber that can store the address of a variable of type long:

```
long* pnumber {};        // A pointer to type long
```

The type of pnumber is “pointer to long,” which is written as long*. This pointer can only store an address of a variable of type long. An attempt to store the address of a variable that is other than type long will not compile. Because the initializer is empty, the statement initializes pnumber with the pointer equivalent of zero, which is a special address that doesn't point to anything. This special pointer value is written as nullptr, and you could specify this explicitly as the initial value:

```
long* pnumber {nullptr};
```