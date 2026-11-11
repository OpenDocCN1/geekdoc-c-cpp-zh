```
}
}
```

# Selective catching

When an exception makes it to the bottom of a block of code without errors, it is handled by the environment. Invalid uses such as inspecting up a property on null, citing a nonexistent binding, or calling a non-function will result in raised exceptions. These exceptions can be caught. JavaScript does not support selective catching of exceptions. Below is an example that tries to continue calling promptDirection until it provides a valid answer:

```
for (;;) {
  try {
    let dir = promptDirection("Where?"); // ← typo!
    console.log("You select ", dir);
    break;
  } catch (e) {
    console.log("Invalid direction. Try again.");
  }
}
```

The for (;;) construct is used to build a loop that cannot be terminated on its own. You can break out of the loop when you have a valid direction, but a misspelled promptDirection will output an undefined variable error. If you want to catch a particular type of exception, check in the catch block if the exception you have is the same one you want and rethrow it. Let’s describe a new kind of error and utilize instance of to recognize it.

```
class InputError extends Error {}
function promptDirection(question) {
  let result = prompt(question);
  if (result.toLowerCase() == "left") return "L";
  if (result.toLowerCase() == "right") return "R";
  throw new InputError("Invalid direction: " + result);
}
```

The new error class prolongs error. It does not describe its own constructor, it inherits the Error constructor, which anticipates a string message that we can recognize it with.

Now the loop can catch these more carefully.

```
for (;;) {
  try {
    let dir = promptDirection("Where?");
```