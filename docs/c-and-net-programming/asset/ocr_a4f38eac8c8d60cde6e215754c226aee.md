# Explanation

2. The most basic expression consists of an *operator*, two *operands* and an *assignment*. The following is an example of an expression.

```
int sum = 10 + 20;
```
In the above example the (+) operator is used to add two operands (10 and 20 which are constants).. The *assignment operator* (=) then assigns the result of the addition to an integer variable named sum. The operands could just have easily been variables or constants (or a mixture of each) instead of the actual numerical values.

3. Expressions can consist of a literal value, a method invocation, an operator and its operands, or a *simple name*. Simple names can be the name of a variable, type member, method parameter, namespace or type.

4. Expressions can use operators that in turn use other expressions as parameters, or method calls whose parameters are in turn other method calls, so expressions can range from simple to very complex.

# Example

+   1. `((x < 20) && (x > 15)) || ((x > 10) && (x < 50))`
+   2. `System.Convert.ToInt32("456")`

5. In most of the contexts where expressions are used, the expression is expected to evaluate to some value.

6. If num1 and num2 are integers, the expression `num1 * num2` evaluates to a numeric value.

7. The expression `new NumberClass()` evaluates to a reference to a new instance of a NumberClass object.

8. The expression `numberclass.ToString()` evaluates to a string because that is the return type of the method.

9. It should be noted that, although a *namespace* name is classified as an expression, it does not evaluate to a value and therefore can never be the final result of any expression. One cannot pass a namespace name to a method parameter, or use it in a new expression, or assign it to a variable. One can only use it as a sub-expression in a larger expression. The same is true for *types* (as distinct from *System.Type* objects), method group names (as distinct from specific methods), and even *add and remove accessors*.

10. Every evaluated value has an associated type. For example, if num1 and num2 are both variables of type int, the value of the expression `num1 + num2` is also typed as `int`. If this value is assigned to a variable of a different type, or if num1 and num2 are different of types, the rules of Casting and Type Conversions are applied.