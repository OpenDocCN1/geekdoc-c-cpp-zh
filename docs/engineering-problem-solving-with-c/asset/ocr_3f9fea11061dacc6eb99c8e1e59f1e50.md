The string object salutation has a size, or length, of five. The string object name has a size of eight. The size of a string object may change during execution. For example, if the assignment statement

```
salutation = "Goodbye";
```

were added to program chapter2_2, the memory snapshot would be modified and the size of salutation would change to seven.

```
string salutation Goodbye
```

```
string name Jane Doe
```

# Symbolic Constants

A symbolic constant is defined using the const modifier. Engineering constants such as pi or the acceleration of gravity are good candidates for symbolic constants. For example, consider the following declaration statement to assign a value to the symbolic constant PI:

```
const double PI = acos(-1.0);
```

The acos function, when evaluated at -1, will return an approximation for pi that includes 15 digits of precision. Statements that need to use the value of pi would then use the symbolic constant PI as illustrated in this statement:

```
area = PI*radius*radius;
```

which computes the area of a circle.

Symbolic constants are usually defined with uppercase identifiers (as in PI instead of pi) to indicate that they are symbolic constants, and, of course, the identifiers should be selected so that they are easy to remember. Once an identifier has been declared and initialized using the const modifier, its value cannot be changed within the program.

# Auto Type Specifier

The C++11 keyword auto supports the declaration of an object without specifying a data type, as long as an initializer is provided. The data type of the initializer defines the data type of the identifier. When using the keyword auto, it is preferred to use the = notation for initialization. Consider the following type declaration statements:

```
auto x1 = 0;        //x1 is type integer
auto comma = ',',   //comma is type char
auto y1 = 0.5;      //y1 is type double
auto count{0};      //count is type initializer_list<int>
```

The keyword auto acts like a placeholder for the data type of the initializer. In the case of auto count{0}; the initializer {0} is interpreted as an initializer list of type integer, not an integer. There is no advantage to using auto for the simple declaration of built-in types, but it can be useful as data types become more complex, and harder to determine.