```
char choice;
cin >> choice;

if (choice >= firstChoice && choice <= lastChoice)
    break;

cerr << "\nI'm sorry, but " << choice
    << " is not a valid menu choice.\n";
}
return choice;        // ERROR!
}
```

When this function is compiled, the return statement generates an error message like

```
Identifier 'choice' is undeclared
```

(Before continuing, try to find the cause of the error using the scope rules.)

The problem is that by Scope Rule S1, the scope of choice only runs through the last statement of the block that is the body of the loop. Because the return statement appears after the block, it lies outside the scope of choice, and so the compiler generates an error when it attempts to access choice. The problem can be avoided by moving the declaration of choice to the outermost block of the function, thus ensuring that all statements that refer to choice lie within its scope:

```
char getMenuChoice(const string& MENU, char firstChoice, char lastChoice)
{
    char choice;
    for (;;)
    {
        cout << MENU;
        cin >> choice;

        if (choice >= firstChoice && choice <= lastChoice)
            break;

        cerr << "\nI'm sorry, but " << choice
            << " is not a valid menu choice.\n";
    }
    return choice;            // OK!
}
```

# 10.4.1.2 Objects Declared Outside All Blocks

Although we have not put any declarations of variables or constants outside all blocks, we have done so with prototypes of functions and with libraries that are included in a program. For example, in Example 10.5, the prototype of the function chopIPAddress() precedes the main function, so that the identifier chopIPAddress is declared outside all blocks. By Scope Rule S4, its scope thus extends from its declaration to the end of the file.