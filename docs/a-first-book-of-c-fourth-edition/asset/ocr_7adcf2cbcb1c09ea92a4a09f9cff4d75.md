```
return 0;
}

void valfun()  // no values are passed to this function
{
    int secnum;  // create a second local variable named secnum

    secnum = 30;  // this only affects this local variable's value

    cout << "\nFrom valfun(): firstnum = " << firstnum << endl;
    cout << "From valfun(): secnum = " << secnum << endl;

    firstnum = 40;    // changes firstnum for both functions

    return;
}
```

The variable firstnum in Program 6.11 is a global variable because its storage is created by a definition statement located outside a function. Because both main() and valfun() follow the definition of firstnum, both functions can use this global variable with no further declaration needed.

Program 6.11 also contains two separate local variables, both named secnum. Storage for the secnum variable named in main() is created by the definition statement in main(). A different storage area for the secnum variable in valfun() is created by the definition statement in the valfun() function. Figure 6.11 shows the three distinct storage areas reserved by the three definition statements in Program 6.11.

Each variable named secnum is local to the function in which its storage is created, and each variable can be used only from within its corresponding function. Therefore, when secnum is used in main(), the storage area main() reserves for its secnum variable is accessed, and when secnum is used in valfun(), the storage area valfun() reserves for its secnum variable is accessed. The following output is produced when Program 6.11 runs:

```
From main(): firstnum = 10
From main(): secnum = 20

From valfun(): firstnum = 10
From valfun(): secnum = 30

From main() again: firstnum = 40
From main() again: secnum = 20
```

Now analyze this output to see how local and global variables work. Because firstnum is a global variable, both main() and valfun() can use and change its value. Initially, both functions print the value of 10 that main() stored in firstnum. Before returning, valfun() changes the value of firstnum to 40, which is the value displayed when firstnum is next displayed from within main().