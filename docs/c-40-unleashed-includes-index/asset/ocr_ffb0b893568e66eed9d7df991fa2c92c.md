![](bbox=[0.1, 0.08, 0.35, 0.65])

FIGURE 17.13 An extensible calculator.

Besides typical arithmetic operations like add, subtract, multiply, divide, and modulo, four additional programmable function keys are provided. The way the programming is done is something you can dream about, but what's more interesting is how to create a generic calculator engine in which those custom operations can be plugged.

Let's try to define a Calculator class to provide the core calculator engine:

```
class Calculator {
    public int Add(int a, int b) { return a + b; }
    public int Sub(int a, int b) { return a - b; }
    public int Mul(int a, int b) { return a * b; }
    public int Div(int a, int b) { return a / b; }
    public int Mod(int a, int b) { return a % b; }
}
```

The problem with this first attempt is clear: It doesn't allow for custom functions to be plugged in, other than deriving from the Calculator class and providing methods for the additional functions you want. That by itself causes a bigger problem, though: How can the UI of the calculator discover those new operations easily?

Not only this, but given the preceding Calculator definition, how would you implement an evaluator? Suppose the user enters the following key sequence:

1, 2, +, 3, 4, =