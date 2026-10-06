function definitions in the header file. If the function's body had been longer, we would put a function prototype in the header file and the function definition (without the) inline .cpp file.

The following code snippet shows all overloaded operators in action:

```
Point2D alpha(12.5, 40.0);
Point2D beta(77.5, 50.0);
```

```
alpha += beta;
beta -= alpha;
```

```
Point2D gamma = alpha + beta;
Point2D delta = beta - alpha;
```

We can also invoke the operator functions just like any other functions:

```
Point2D alpha(12.5, 40.0);
Point2D beta(77.5, 50.0);
```

```
alpha.operator+=(beta);
beta.operator-=(alpha);
```

```
Point2D gamma = operator+(alpha, beta);
Point2D delta = operator-(beta, alpha);
```

Operator overloading in C++ is a complex topic, but we can go a long way without knowing all the details. It is still important to understand the fundamentals of operator overloading because several Qt classes (including QString and QVector<T>) use this feature to provide a simple and more natural syntax for such operations as concatenation and append.

# Value Types

Java and C# distinguish between value types and reference types.

+   * Value types: These are primitive types as char, int, and float, as well as C# structs. What characterizes them is that they aren't created using new and the assignment operator performs a copy of the value held by the variable. For example:

```
int i = 5;
int j = 10;
i = j;
```