This initialization goes in the methods file, not in the class declaration file. That's because the class declaration is in a header file, and a program may include a header file in several other files. That would result in multiple copies of the initialization statement, which is an error.

The exception to the noninitialization of a static data member inside the class declaration (see Chapter 10, "Objects and Classes") is if the static data member is a const of integral or enumeration type.

> > **Note**
> > A static data member is declared in the class declaration and is initialized in the file containing the class methods. The scope operator is used in the initialization to indicate to which class the static member belongs. However, if the static member is a const integral type or an enumeration type, it can be initialized in the class declaration itself.

Next, notice that each constructor contains the expression num_strings++. This ensures that each time a program creates a new object, the shared variable num_strings increases by one, keeping track of the total number of String objects. Also the destructor contains the expression --num_strings. Thus, the String class also keeps track of deleted objects, keeping the value of the num_strings member current.

Now look at the first constructor in Listing 12.2, which initializes a String object with a regular C string:

```
```
StringBad::StringBad(const char * s)
{
    len = std::strlen(s);          // set size
    str = new char[len + 1];       // allot storage
    std::strcpy(str, s);           // initialize pointer
    num_strings++;                 // set object count
    cout << num_strings << ": \"" << str
         << "\" object created\n"; // For Your Information
}
```
```

Recall that the class str member is just a pointer, so the constructor has to provide the memory for holding a string. You can pass a string pointer to the constructor when you initialize an object:

```
`String boston("Boston");`
```

The constructor must then allocate enough memory to hold the string, and then it must copy the string to that location. Let's go through the process step-by-step.

First, the function initializes the len member, using the strlen() function to compute the length of the string. Next, it uses new to allocate sufficient space to hold the string, and then it assigns the address of the new memory to the str member. (Recall that strlen() returns the length of a string, not counting the terminating null character, so the constructor adds one to len to allow space for the string, including the null character.)