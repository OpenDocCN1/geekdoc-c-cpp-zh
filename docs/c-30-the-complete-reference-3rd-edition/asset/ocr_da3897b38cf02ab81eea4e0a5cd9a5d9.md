```
// Point p to start of str.
fixed(char* p = str) {
    // Display the contents of str via p.
    for(int i=0; p[i] != 0; i++)
        Console.Write(p[i]);
}

Console.WriteLine();
}
```

The output is shown here:

```
this is a test
```

# Multiple Indirection

You can have a pointer point to another pointer that points to the target value. This situation is called multiple indirection, or pointers to pointers. Pointers to pointers can be confusing. Figure 20-1 helps clarify the concept of multiple indirection. As you can see, the value of a normal pointer is the address of the variable that contains the value desired. In the case of a pointer to a pointer, the first pointer contains the address of the second pointer, which points to the variable that contains the value desired.

Multiple indirection can be carried on to whatever extent desired, but more than a pointer to a pointer is rarely needed. In fact, excessive indirection is difficult to follow and prone to conceptual errors.

A variable that is a pointer to a pointer must be declared as such. You do this by placing an additional asterisk after the type name. For example, the following declaration tells the compiler that q is a pointer to a pointer of type int:

```
int** q;
```

You should understand that q is not a pointer to an integer, but rather a pointer to an int pointer.

![](bbox=[0.3, 0.65, 0.9, 0.9])