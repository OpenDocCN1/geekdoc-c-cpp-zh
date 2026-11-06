# Preventing Implicit Conversions with Single-Argument Constructors

The reason we’ve been declaring every single-argument constructor preceded by the keyword `explicit` is to *suppress implicit conversions via conversion constructors when such conversions should not be allowed*. A constructor that’s declared `explicit` cannot be used in an implicit conversion. In the example of **Figure 10.13**, we use the original version of `Array.h` from **Fig. 10.10**, which included the keyword `explicit` in the declaration of the *single-argument constructor* in line 13

```
```cpp
explicit Array(int = 10); // default constructor
```
```

**Figure 10.13** presents a slightly modified version of the program in **Fig. 10.12**. When this program in **Fig. 10.13** is compiled, the compiler produces an error message, such as

```
```
'void outputArray(const Array &)': cannot convert argument 1
from 'int' to 'const Array &'
```
```