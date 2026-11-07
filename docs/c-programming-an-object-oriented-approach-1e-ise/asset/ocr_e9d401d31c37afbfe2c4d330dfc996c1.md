# Program 9.4  Printing size, value, and addresses (Continued)

```
```cpp
// Printing size, value, and address of the score variable
cout << "A variable of type int" << endl;
cout << "Size: " << sizeof(score) << " ";
cout << "Value: " << score << " ";
cout << "Address: " << &score << endl << endl;
// Printing size, value, and address of the average variable
cout << "A variable of type double" << endl;
cout << "Size: " << sizeof(average) << " ";
cout << "Value: " << average << " ";
cout << "Address: " << &average << endl;
return 0;
}
```
```

```
Run:
A variable of type bool
Size: 1  Value: 1  Address: 0x28fef0

A variable of type int
Size: 4  Value: 92  Address: 0x28fef1

A variable of type double
Size: 8  Value: 82.56  Address: 0x28fef5
```

There are three important points about Program 9.4:

+   - The extraction operator (`<<`) is overloaded so that it can accept an address. Therefore, we can use the expression `cout << &score` to print the address of the variables.
+   - The addresses are displayed using hexadecimal notation. The addresses are not integers; they are pointer types, as we will see shortly.
+   - The sizes and addresses may be different in different systems. The address may start from the smallest to largest or vice versa. There may be some gaps in the addresses.

Figure 9.8 shows the addresses as printed in Program 9.5.

![](bbox=[0.328, 0.746, 0.748, 0.888])

Figure 9.8  Memory situation declared and defined in Program 9.5