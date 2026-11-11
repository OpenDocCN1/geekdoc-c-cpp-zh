outer function. The set of bindings accessible within a block is decided by the block position in the program text. Every local scope can access the contained local scope and every scope can as well access the global scope. This concept is named lexical scoping.

# Functions as values

A function binding often behaves as a name for a particular block of program. This type of binding does not change because it is defined. Functions can be used in arbitrary expressions as well as used to save a function value into a new binding. A binding that stores a function is a systematic binding and a new value can be assigned like:

```
let launchMissiles = function() {
  missileSystem.launch("now");
};
if (safeMode) {
  launchMissiles = function() {/* do nothing */};
}
```

# Declaration notation

There is a little way to generate a function binding. When you use the function keyword at the beginning of a statement, it will function differently.

```
function square(x) {
  return x * x;
}
```

This statement describes the binding square and directs it at a stated function. This type of function definition consists of one precision.

```
console.log("My mind tells me every time:", future());
function future() {
  return "I'll surpass Bill Gates";
}
```

# Arrow functions

Functions contains a third notation that does not look identical to the others. You can use the arrow (=>) as an alternative to the function keyword. The arrow (=>) contains an equal sign and the greater than character.

```
const power = (base, exponent) => {
  let result = 1;
  for (let count = 0; count < exponent; count++) {
    result *= base;
  }
  return result;
}
```