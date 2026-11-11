```
```javascript
function repeatLog(n) {
  for (let I = 0; I < n; I++) {
    console.log(I);
  }
}
```
```

If you want to perform a task different from logging in numbers, you can roll action as a function value.

```
```javascript
function repeat(n, action) {
  for (let I = 0; I < n; I++) {
    action(i);
  }
}

repeat(3, console.log);
// → 0
// → 1
// → 2
```
```

Sometimes you do not need to roll in a predefined function to repeat in a loop, create a function value as an alternative:

```
```javascript
let labels = [];
repeat(5, i => {
  labels.push(`Unit ${i + 1}`);
});
console.log(labels);
// → ["Unit 1", "Unit 2", "Unit 3", "Unit 4", "Unit 5"]
```
```

This method layout looks similar to a loop; it defines the type of loop and then produce a body. Although the body is written in function enclosed in parentheses of the call to repeat.

# Higher-order functions

Higher-order functions are functions that work on other functions whether by arguments or by sending them back. This type of function enables user to abstract over actions. For instance, you have a function that can produce functions

```
```javascript
function greaterThan(n) {
  return m => m > n;
}

let greaterThan10 = greaterThan(10);
console.log(greaterThan10(11));
// → true
```
```

You can also have functions that can transform other functions.