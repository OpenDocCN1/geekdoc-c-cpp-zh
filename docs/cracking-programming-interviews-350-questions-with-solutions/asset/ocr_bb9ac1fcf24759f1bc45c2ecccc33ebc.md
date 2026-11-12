# Solution of Question 121

This code doesn't get compiled. Compiler error is

```
```
scoped_enum1.cpp:5:9: error: cannot initialize a
  variable of type 'int' with an
    rvalue of type 'Color'
    int r = Color::red;
        ^~~~~~~~~
scoped_enum1.cpp:9:9: error: value of type
  'Color' is not contextually
    convertible to 'bool'
    if (r1) { }
        ^

2 errors generated.
```
```

Another compiler gives the error below:

```
```
scoped_enum1.cpp: In function 'int main()':
scoped_enum1.cpp:5:20: error: cannot convert
  'Color' to 'int' in initialization
    int r = Color::red;
        ^
scoped_enum1.cpp:9:11: error: could not convert
  'r1' from 'Color' to 'bool'
    if (r1) { }
        ^
```
```

Please note that implicit enum to any other type like int or bool con-
version is not provided for a scoped enumeration.