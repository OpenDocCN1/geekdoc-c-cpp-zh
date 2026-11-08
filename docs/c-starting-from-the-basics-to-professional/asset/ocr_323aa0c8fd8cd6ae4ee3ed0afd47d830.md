```
```cpp
std::cout << std::format("The value of the expression {} < {} is {}\n",
                         first, second, first < second);
std::cout << std::format("The value of the expression {} == {} is {}\n",
                         first, second, first == second);
```
```

# Comparing Floating-Point Values

Of course, you can also compare floating-point values. Let’s consider some slightly more complicated numerical comparisons. First, define variables with the following statements:

```
```cpp
int i {-10};
int j {20};
double x {1.5};
double y {-0.25e-10};
```
```

Now consider the following logical expressions:

```
```cpp
-1 < y        j < (10 - i)        0.0*x > (3 + y)
```
```

The comparison operators are all of lower precedence than the arithmetic operators, so none of the parentheses are strictly necessary, but they do help make the expressions clearer. The first comparison evaluates to true because y has a very small negative value (~−0.000000000025), which is greater than −1. The second comparison results in false because the expression 10 − i has the value 20, which is the same as j. The third expression is true because 3 + y is slightly less than 3.

One peculiarity about floating-point comparisons is that not-a-number values are neither less than, greater than, nor equal to any other number. They’re not even equal to another not-a-number value. Let the nan variable be defined as follows (see Chapter 2 for the numeric_limits template):

```
```cpp
const double nan{ std::numeric_limits<double>::quiet_NaN() };
```
```

Then all of the following expressions evaluate to false:

```
```cpp
i < nan     nan > j     nan == nan
```
```

You can use relational operators to compare values of any of the fundamental types. When you learn about classes, you’ll see how you can arrange for the comparison operators to work with types that you define, too. All you need now is a way to use the result of a comparison to modify the behavior of a program. We’ll look into that shortly. But first: a visit from our outer space...

# The Spaceship Operator

In C++20, a new operator was added to the language to compare values: the three-way comparison operator, denoted <=>. This new operator is better known by its informal name: spaceship operator. It gets this nickname from the fact that the character sequence <=> somewhat resembles a flying saucer!