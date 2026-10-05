```
int main() {
    int input;
    cout << "Please enter an integer";
    cin >> input;
    if (input = 2)
        cout << "two" << endl;
    cout << "You entered " << input << endl;
}
```

Listing 5.7 (badquality.cpp) demonstrates a common mistake—using the assignment operator where the equality operator is intended. When run, it always prints the message "two" and insists that the user entered 2 regardless of the actual input. Recall from Section 4.3 that the assignment expression has a value. The value of an assignment expression is the same as the value that is assigned; thus, the expression

input = 2

has the value. You also consider that any integer can be treated as a Boolean value (See Section 5.1) and any non-zero value is interpreted as true, you can see that the condition of if statement

```
if (input = 2)
    cout << "two" << endl;
```

is always true. Additionally, the variable input assigns the value 2.

Since it is such a common coding error, most C++ compilers check for such misuse of assignment. At warning Level 4, C++ will issue a warning when assignment appears within a conditional expression is expressed:

> warning C4706: assignment within conditional expression

Occasionally the use of assignment within a conditional expression is warranted, the compiler does not perform this check by default. For our purposes it is good to direct the compiler to perform this extra check.

Carefully consider each compound conditional, such as

```
x > 0 && x <= 10
```

found in Listing 5.7 (newchangerange.cpp). Confusing logical and logical is a common programming error. If you use || &&, the expression

```
x > 0 || x <= 10
```

is always true, not value is assigned to the variable x. A Boolean expression that is always true is known as a tautology. Think about it. If x is an int, what value could the variable x assume that would make

```
x > 0 || x <= 10
```

false? Regardless of its value, or both of the subexpressions will be true, this compound logical or expression is true. This particular expression is just a complicated way of expressing the value true.

Another common error is constructing Boolean expressions that are always false, contradictions. Suppose you wish to exclude values from a range; for example, reject values in the