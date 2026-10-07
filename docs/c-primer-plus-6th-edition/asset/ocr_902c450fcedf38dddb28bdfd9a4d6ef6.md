```
// construct String from C string
String::String(const char * s)
{
    len = std::strlen(s);                // set size
    str = new char[len + 1];            // allot storage
    std::strcpy(str, s);                 // initialize pointer
    num_strings++;                       // set object count
    cout << num_strings << " "\"" << str
         << "\"" object created\n";     // For Your Information
}
```

```
String::String()                              // default constructor
{
    len = 4;
    str = new char[4];
    std::strcpy(str, "C++");             // default string
    num_strings++;
    cout << num_strings << " "\"" << str
         << "\"" object created\n";     // FYI
}
```

```
String::~String()                      // necessary destructor
cout << "\"" << str << "\"" object deleted, "; // FYI
    --num_strings;                        // required
cout << num_strings << " " left\n";     // FYI
delete [str];                          // required
```

```
std::ostream& operator<<(std::ostream& os, const StringBad & os)
{
    os << os.str;
    return os;
}
```

First, notice the following statement from Listing 12.2:
int String::num_strings = 0;

This statement initializes the static num_strings member to 0. Note that you cannot initialize a static member variable inside the class declaration. That's the declaration is a description of how memory is allocated but it doesn't allocate memory.You allocate and initialize memory by creating an object using that format. In the case of a static member, you initialize the static member independently, with a separate statement outside the class declaration. Note that the static class member is stored separately rather as part of an object. The initialization statement gives the type and uses the scope operator, but it doesn't use the static keyword.