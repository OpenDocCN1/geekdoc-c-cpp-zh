# The Return Values

Writing information on the screen and displaying dialog boxes are known as side effects. Because of these side effects, functions are important in the JavaScript language. You may also use functions to generate values – in this case, a function can be useful even without its side effects. For instance, Math.max (a JavaScript function) receives an unlimited number of numeric values and indicates the highest one. Here ’ s an example:

```
console.log(Math.max(1, 2, 3, 4, 5));
// -> 5
```

In JavaScript, anything that generates values is considered as an expression. That means you can perform function calls in large expressions. In the example below, you ’ ll use the Math.min function as an input for the “ + ” operator:

```
console.log(Math.min(1, 2) + 98);
// -> 99
```