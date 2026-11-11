# for loops

A lot of loops follow the while loop pattern, creating a counter binding to track the loop's progress. Then a while loop with a test expression to see if the counter reaches the set value.

```
for (let number = 0; number <= 10; number = number + 4) {
  console.log(number);
}
// → 0
// → 4
// etc
```

The parentheses must consist of two semicolons after the keyword, the first part that is before the first semicolon separates the loop by describing a binding. The other part is the statement that determines if the loop should continue. Here is the code that evaluate 210 using for instead of while:

```
let result = 1;
for (let counter = 0; counter < 10; counter = counter + 1) {
  result = result * 2;
}
console.log(result);
// → 1024
```

# Breaking Out of a Loop

There are other ways to end a loop other than making a looping condition give a false. Break can influence jumping out of the confined loop. The break statement evaluates this program if the first number, which is both greater than or equal to 20, and can be divided by 7.

```
for (let current = 20; current = current + 1) {
  if (current % 7 == 0) {
    console.log(current);
    break;
  }
}
// → 21
```

The (%) operator is used to check if a number can be divided by another number. If it can be divided, then the remaining division is zero. The for in the example is