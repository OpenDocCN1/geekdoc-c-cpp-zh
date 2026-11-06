# 21.12 String Stream Processing

In addition to standard stream I/O and file stream I/O, C++ stream I/O includes capabilities for inputting from, and outputting to, `strings` in memory. These capabilities often are referred to as **in-memory I/O** or **string stream processing**.

Input from a `string` is supported by class `istringstream`. Output to a `string` is supported by class `ostringstream`. The class names `istringstream` and `ostringstream` are actually aliases defined by the `typedef`s

```
```cpp
typedef basic_istringstream< char > istringstream;
typedef basic_ostringstream< char > ostringstream;
```
```

Class templates `basic_istringstream` and `basic_ostringstream` provide the same functionality as classes `istream` and `ostream` plus other member functions specific to *in-memory formatting*. Programs that use in-memory formatting must include the `<sstream>` and `<iostream>` headers.