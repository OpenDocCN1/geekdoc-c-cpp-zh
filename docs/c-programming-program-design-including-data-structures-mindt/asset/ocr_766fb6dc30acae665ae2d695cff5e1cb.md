```
```
char* newString::strcopy(const char *str)
{
    for (int i = 0; i < strLength; i++)
        strPtr[i] = str[i];
    strPtr[strlength] = '\0';

    return strPtr;
}

char* newString::strcopy(char * str1, const char *str2)
{
    for (int i = 0; i < strlen(str1); i++)
        str1[i] = str2[i];
    str1[strlen(str1)] = '\0';

    return str1;
}
```
```

Consider the statement

```
```
isObject >> setw(81) >> temp;
```
```

in the definition of the function `operator>>`. Because `temp` is declared to be an array of size 81, the largest string that can be stored into `temp` is of length 80. The manipulator `setw` in this statement (that is, in the input statement) ensures that no more than 80 characters are read into `temp`.

Most of these functions are quite straightforward. Let us explain the functions that overload the conversion constructor, the assignment operator, and the copy constructor.

The conversion constructor is a single-parameter function that converts its argument to an object of the constructor's class. In our case, the conversion constructor converts a string to an object of the `newString` type.

Note that the assignment operator is explicitly overloaded only for objects of the `newString` type. However, the overloaded assignment operator also works if we want to store a C-string into a `newString` object. Consider the declaration

```
```
newString str;
```
```

and the statement

```
```
str = "Hello there";
```
```

The compiler translates this statement into

```
```
str.operator=("Hello there");
```
```

+   1. First, the compiler automatically invokes the conversion constructor to create an object of the `newString` type to temporarily store the string "Hello there".
+   2. Second, the compiler invokes the overloaded assignment operator to assign the temporary `newString` object to the object `str`.