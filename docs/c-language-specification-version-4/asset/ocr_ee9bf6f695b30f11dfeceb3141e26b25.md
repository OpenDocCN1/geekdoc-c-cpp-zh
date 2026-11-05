```
public VariableReference(string name) {
    this.name = name;
}
public override double Evaluate(Hashtable vars) {
    object value = vars[name];
    if (value == null) {
        throw new Exception("Unknown variable: " + name);
    }
    return Convert.ToDouble(value);
}
public class Operation: Expression
{
    Expression left;
    char op;
    Expression right;
    public Operation(Expression left, char op, Expression right) {
        this.left = left;
        this.op = op;
        this.right = right;
    }
    public override double Evaluate(Hashtable vars) {
        double x = left.Evaluate(vars);
        double y = right.Evaluate(vars);
        switch (op) {
            case '+': return x + y;
            case '-': return x - y;
            case '*': return x * y;
            case '/': return x / y;
        }
        throw new Exception("Unknown operator");
    }
}
```

The previous four classes can be used to model arithmetic expressions. For example, using instances of these classes, the expression x + 3 can be represented as follows.

```
Expression e = new Operation(
    new VariableReference("x"),
    '+',
    new Constant(3));
```

The Evaluate method of an Expression instance is invoked to evaluate the given expression and produce a double value. The method takes as an argument a Hashtable that contains variable names (as keys of the entries) and values (as values of the entries). The Evaluate method is a virtual abstract method, meaning that non-abstract derived classes must override it to provide an actual implementation.

A Constant's implementation of Evaluate simply returns the stored constant. A VariableReference's implementation looks up the variable name in the hashtable and returns the resulting value. An Operation's implementation first evaluates the left and right operands (by recursively invoking their Evaluate methods) and then performs the given arithmetic operation.

The following program uses the Expression classes to evaluate the expression x * (y + 2) for different values of x and y

```
using System;
using System.Collections;
class Test
{
    static void Main() {
```