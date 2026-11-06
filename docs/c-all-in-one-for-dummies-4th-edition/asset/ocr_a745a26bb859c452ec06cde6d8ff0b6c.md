and you are free to use the argv variable to access an array of pointers — specifically, in this case, an array of character pointers, also called *strings*.

# Building constant arrays

If you have an array and you don’t want its contents to change, you can make it a constant array. The following lines of code, found in the Array05 example, demonstrate this approach:

```
const int Permanent[5] = { 1, 2, 3, 4, 5 };
cout << Permanent[1] << endl;
```

This array works like any other array, except you cannot change the numbers inside it. If you add a line like the following line, you get a compiler error, because the compiler is aware of constants:

```
Permanent[2] = 5;
```

Here’s the error you get when working in Code::Blocks:

```
error: assignment of read-only location 'Permanent[2]'
```

Arrays have a certain constancy built in. For example, you can’t assign one array to another. If you make the attempt (as shown in the Array06 example), the Code::Blocks compiler presents you with an error: invalid array assignment error message.)

```
int NonConstant[5] = { 1, 2, 3, 4, 5 };
int OtherList[5] = { 10, 11, 12, 13, 14 };
OtherList = NonConstant;
```

In other words, that third line is saying, “Forget what OtherList points to; instead, make it point to the NonConstant array, {1,2,3,4,5}!” The point is that arrays are always constant. If you want to make the array elements constant, you can precede its type with the word const. When you do so, the array name is constant, and the elements inside the array are also constant.

# Pointing with Pointers

To fully understand C++ and all its strangeness and wonders, you need to become an expert in pointers. (Fortunately, many modern innovations in C++ are making the need to know pointers less of an issue — you have other means at your