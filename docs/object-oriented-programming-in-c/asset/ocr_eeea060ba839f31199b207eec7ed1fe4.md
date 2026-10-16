```
{
    case circle:
        .....
        .....
        break;
    case rectangle:
        .....
        .....
        break;
    case triangle:
        .....
        .....
        break;
}
    cout << "Enter shape code:";
    cin >> code;
}
cout << "BYE \n";

return 0;
}
```

ANSI C permits an enum to be defined within a structure or a class, but the enum is globally visible. In C++, an enum defined within a class (or structure) is local to that class (or structure) only.

# 3.7 Derived Data Types

# Arrays

The application of arrays in C++ is similar to that in C. The only exception is the way character arrays are initialized. When initializing a character array in ANSI C, the compiler will allow us to declare the array size as the exact length of the string constant. For instance,

```
char string[3] = "xyz";
```

is valid in ANSI C. It assumes that the programmer intends to leave out the null character \0 in the definition. But in C++, the size should be one larger than the number of characters in the string.

```
char string[4] = "xyz"; // O.K. for C++
```

# Functions

Functions have undergone major changes in C++. While some of these changes are simple, others require a new way of thinking when organizing our programs. Many of these