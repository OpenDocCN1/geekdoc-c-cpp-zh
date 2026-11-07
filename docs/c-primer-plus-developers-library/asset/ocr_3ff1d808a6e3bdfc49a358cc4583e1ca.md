```
~~~cpp
cout << "*ps = " << ps << ", *ps = " << *ps << endl;
ps = ps + 1;
cout << "add 1 to the ps pointer:\n";
cout << "*ps = " << ps << ", *ps = " << *ps << "\n\n";

cout << "access two elements with array notation\n";
cout << "stacks[0] = " << stacks[0]
     << ", stacks[1] = " << stacks[1] << endl;
cout << "access two elements with pointer notation\n";
cout << "*stacks = " << *stacks
     << ", *(stacks + 1) = " << *(stacks + 1) << endl;

cout << sizeof(wages) << " = size of wages array\n";
cout << sizeof(pw) << " = size of pw pointer\n";
return 0;
}
~~~
```

Here is the output from the program in Listing 4.19:

```
~~~text
pw = 0x28ccf0, *pw = 10000
add 1 to the pw pointer:
pw = 0x28ccf8, *pw = 20000

ps = 0x28ccea, *ps = 3
add 1 to the ps pointer:
ps = 0x28ccec, *ps = 2

access two elements with array notation
stacks[0] = 3, stacks[1] = 2
access two elements with pointer notation
*stacks = 3, *(stacks + 1) = 2
24 = size of wages array
4 = size of pw pointer
~~~
```

# ## Program Notes

In most contexts, C++ interprets the name of an array as the address of its first element. Thus, the following statement makes pw a pointer to type double and then initializes pw to wages, which is the address of the first element of the wages array:

```
~~~cpp
double * pw = wages;
~~~
```

For wages, as with any array, we have the following equality:

```
~~~text
wages = wages[0] = address of first element of array
~~~
```

Just to show that this is no jive, the program explicitly uses the address operator in the expression &stacks[0] to initialize the ps pointer to the first element of the stacks array.