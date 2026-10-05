# 11.1. VECTORS

```
vector<int> vec_a;
vector<int> vec_b(10);
vector<int> vec_c(10, 8);
vector<int> vec_d( 10, 20, 30, 40 );
```

vec_a

![](bbox=[0.262, 0.276, 0.303, 0.316])

vec_b

| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

vec_c

| 8 | 8 | 8 | 8 | 8 | 8 | 8 | 8 | 8 | 8 |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

vec_d

| 10 | 20 | 30 | 40 |
| 0 | 1 | 2 | 3 |

Figure 11.1: Four different vector declaration statements and conceptual illustrations of the resulting vectors

Like any other variable, a vector can be local or global, and it must be declared before it is used.

> The vector initializes list:
vector<int> vec_d{10, 20, 30, 40};
is a C++11 language feature and, therefore, is not supported by older C++ compilers; in particular, the C++ compilers for Visual Studio editions prior to Visual Studio 2013 do not support this initializer syntax.

When we have a non-empty vector object, we can access its elements using the array's name, the square bracket, and an integer index:

```
vector<int> list(3);      // Declare list to be a vector of three ints
list[0] = 5;               // Make the first element 5
list[1] = -3;              // Make the second element -3
```