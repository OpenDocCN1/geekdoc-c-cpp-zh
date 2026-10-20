# How implicit casting works

# Casting from less precise to more precise data types

byte→short→int→long→decimal

int→double

short→float→double

char→int

# Examples

```
double grade = 93;    // convert int to double
```

```
int letter = 'A';     // convert char to int
```

```
double a = 95.0;
int b = 86, c = 91;
double average = (a+b+c)/3;    // convert b and c to double values
// (average = 90.666666...)
```

# How to code an explicit cast

# The syntax for coding an explicit cast

```
(type) expression
```

# Examples

```
int grade = (int)93.75;          // convert double to int (grade = 93)
```

```
char letter = (char)65;          // convert int to char (letter = 'A')
```

```
double a = 95.0;
int b = 86, c = 91;
int average = ((int)a+b+c)/3;    // convert a to int value (average = 90)
```

```
decimal result = (decimal)b/(decimal)c;    // result has decimal places
```

# Description

+   If you code an assignment statement that assigns a value with a less precise data type to a variable with a more precise data type, C# automatically converts the less precise data type to the more precise data type. This can be referred to as an implicit cast or a widening conversion.

+   No implicit casts can be done between floating-point types and the decimal type.

+   When you code an arithmetic expression, C# implicitly casts operands with less precise data types to the most precise data type used in the expression.

+   To code an assignment statement that assigns a value with a more precise data type to a variable with a less precise data type, you must code the less precise data type in parentheses preceding the value to be assigned. This can be referred to as an explicit cast or a narrowing conversion.

+   You can also use an explicit cast in an arithmetic expression. Then, the casting is done before the arithmetic operations.