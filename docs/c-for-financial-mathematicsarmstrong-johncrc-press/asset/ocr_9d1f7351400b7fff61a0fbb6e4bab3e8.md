![](bbox=[0.24, 0.08, 0.76, 0.2])

**FIGURE 11.3:** A pointer to a memory location containing the null-terminated string Hello.

```
cout << "\n";
}
```

C provides a shortcut for creating a sequence of characters ending with the zero code, just place the desired characters in double quotes. You don't need to include the zero at the end, this is included automatically.

```
const char* charArray2 = "Hello";
for (int i=0; i<6; i++) {
    cout << "ASCII VALUE ";
    char c = charArray2[i];
    cout << ((int)c);
    cout << "\n";
}
```

This format of data is called a “C-style string” or a “null-terminated string”. It is illustrated graphically in Figure 11.3. Note that we have said that the type of charArray2 is const char*. This means that content of the string is fixed.

Earlier in the book we've created strings by writing the text in quotes, but we've tried to avoid the char* data type as far as possible. This is because you should always try to convert a char* into a string as soon as possible.

Since this wasn't possible in C, C contains various functions to help work with null-terminated strings, such as strlen, which computes the length (excluding the terminating zero character) and strcpy, which copies one string into another.

The code below shows how to use pointers directly to replicate the behaviour of the strlen function.

```
int computeLengthOfString( const char* s ) {
    int length = 0;
    while ((**s)!=0) {
        s++;
        length++;
    }
    return length;
```