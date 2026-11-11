a scope object that relate names with values, and it will access the expression that the tree stands for and send back the value that it provides.

```
const specialForms = Object.create(null);
function evaluate(expr, scope) {
  if (expr.type === "value") {
    return expr.value;
  } else if (expr.type === "word") {
    if (expr.name in scope) {
      return scope[expr.name];
    } else {
      throw new ReferenceError(
        `Undefined binding: ${expr.name}`);
    }
  } else if (expr.type === "apply") {
    let {operator, args} = expr;
    if (operator.type === "word" &&
        operator.name in specialForms) {
      return specialForms[operator.name](expr.args, scope);
    } else {
      let op = evaluate(operator, scope);
      if (typeof op === "function") {
        return op(...args.map(arg => evaluate(arg, scope)));
      } else {
        throw new TypeError("Applying a non-function.");
      }
    }
  }
}
```

The evaluator contains codes for every expression type. A literal value expression provides its value. To bind, check if it describes in the scope and, if yes, get the value of the binding. If it contains a unique form that does not access anything, and yet transfers the argument expressions with scope, to the function that influences the form. If the call is typical, access the operator, determine if it is a function, and call it with the accessible arguments. Utilize the common JavaScript function values to stand for the value of Egg’s function. The recursive layout of evaluating is a similar layout of the parser, and the two mirror the layout of the language. You can combine the parser using the evaluator and evaluate when parsing, but separating them gives a clearer of the program. It is all you