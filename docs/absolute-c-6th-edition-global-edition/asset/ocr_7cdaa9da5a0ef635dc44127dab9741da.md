# Display 3.2 Some Predefined Functions

All these predefined functions require using namespace std; as well as an include directive.

| NAME | DESCRIPTION | TYPE OF ARGUMENTS | TYPE OF VALUE RETURNED | EXAMPLE | VALUE | LIBRARY HEADER |
|---|---|---|---|---|---|---|
| sqrt | Square root | double | double | sqrt(4.0) | 2.0 | cmath |
| pow | Powers | double | double | pow(2.0,3.0) | 8.0 | cmath |
| abs | Absolute value for int | int | int | abs(-7) abs(7) | 7 7 | cstdlib |
| labs | Absolute value for long | long | long | labs(-70000) labs(70000) | 70000 70000 | cstdlib |
| fabs | Absolute value for double | double | double | fabs(-7.5) fabs(7.5) | 7.5 7.5 | cmath |
| ceil | Ceiling (round up) | double | double | ceil(3.2) ceil(3.9) | 4.0 4.0 | cmath |
| floor | Floor (round down) | double | double | floor(3.2) floor(3.9) | 3.0 3.0 | cmath |
| exit | End program | int | void | exit(1); | None | cstdlib |
| rand | Random number | None | int | rand() | Varies | cstdlib |
| srand | Set seed for rand | unsigned int | void | srand(42); | None | cstdlib |

Notice that the previous call to pow returns 9.0, not 9. The function pow always returns a value of type double, not of type int. Also notice that the function pow requires two arguments. A function can have any number of arguments. Moreover, every argument position has a specified type, and the argument used in a function call should be of that type. In many cases, if you use an argument of the wrong type, some automatic type conversion will be done for you by C++. However, the results may not be what you intended. When you call a function, you should use arguments of the type specified for that function. One exception to this caution is the automatic conversion of arguments from type int to type double. In many situations, including calls to the function pow, you can safely use an argument of type int (or other integer type) when an argument of type double (or other floating-point type) is specified.