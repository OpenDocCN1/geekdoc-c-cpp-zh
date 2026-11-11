
An exception’s effect is a different type of control flow. This indicates that your code can have different side effects, but an exception could stop them from happening. Below is some bad banking code:

```
const accounts = {
a: 100,
b: 0,
c: 20
};
function getAccount() {
let accountName = prompt("Enter an account name");
if (!accounts.hasOwnProperty(accountName)) {
throw new Error(`No such account: ${accountName}`);
}
return accountName;
}
function transfer(from, amount) {
if (accounts[from] < amount) return;
accounts[from] -= amount;
accounts[getAccount()] += amount;
}
```

The transfer function is used to send a particular sum of money from a stated account to another, as well as demanding for the name of the other account. If you input a wrong account name, getAccount outputs an exception. If the money has been sent from the first account and then the program outputs an exception before it gets the money transferred into the other account, the money will disappear. Solve this problem, utilize the finally block code. This is illustrated below:

```
function transfer(from, amount) {
if (accounts[from] < amount) return;
let progress = 0;
try {
accounts[from] -= amount;
progress = 1;
accounts[getAccount()] += amount;
progress = 2;
} finally {
if (progress === 1) {
accounts[from] += amount;
}
}
}
```

### Selective catching

When an exception makes it to the bottom of a block of code without errors, it is handled by the environment. Invalid uses such as looking up a property on null, citing a nonexistent binding, or calling a non-function will result in raised exceptions. These exceptions can be caught. JavaScript does not support selective catching of exceptions. Below is an example that tries to continue calling promptDirection until it provides a valid answer:

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

The for (;;) construct is used to build a loop that cannot be terminated on its own. You can break out of the loop when you have a valid direction, but a misspelled promptDirection will output an undefined variable error. If you want to catch a particular type of exception, check in the catch block if the exception you have is the same one you want and rethrow it. Let’s describe a new kind of error and utilize instanceof to recognize it.

```
class InputError extends Error {}
function promptDirection(question) {
  let result = prompt(question);
  if (result.toLowerCase() == "left") return "L";
  if (result.toLowerCase() == "right") return "R";
  throw new InputError("Invalid direction: " + result);
}
```

The new error class extends Error. It does not define its own constructor, it inherits the Error constructor, which expects a string message that we can recognize it with.

Now the loop can catch these more carefully.

```
for (;;) {
  try {
    let dir = promptDirection("Where?");
    console.log("You chose ", dir);
    break;
  } catch (e) {
    if (e instanceof InputError) {
      console.log("Invalid direction. Try again.");
    } else {
      throw e;
    }
  }
}
```

### Summary

This chapter deals with debugging. An essential part of programming is identifying and fixing bugs. Sometimes, you can solve problems locally. You can track them with special return values or the use of exceptions.

### Exercise

Fix the below broken code and indicate the problem:

```
for(var I=0; I > 5; I++) {
    console.log(i)
}
```

### Solution

![](img/239ff1e8a63502805c86c4dfbd71509a_738_0.png)

Problem – Incorrect condition within the loop.

## Chapter 10: Regular Expressions

Programming concepts and tools advance in a disorganized way, but their success indicates an excellent piece of technology. In this chapter, we will discuss regular expressions. They are used to define patterns within string data. They are a small, different language that is part of JavaScript as well as other languages.

### Creating a regular expression

A regular expression is constructed with the RegExp constructor or written as a literal value by surrounding a pattern in forward-slash (/) characters.

```
let re1 = new RegExp("ABC");
let re2 = /ABC/;
```

These two regular expression objects stand for the same pattern. When utilizing the RegExp constructor, write the pattern as a normal string so that the rules apply for backslashes.

The second notation treats backslashes differently; you must put a backslash before any forward slash because the pattern appears between slash characters.

### Testing for matches

Regular expression objects contain several methods, one of which is the test. When you pass a string, it returns a Boolean determining if a string contains a match of the pattern in the expression.

```
console.log(/abc/.test("abcde"));
// → true
console.log(/abc/.test("abxde"));
// → false
```

A regular expression contains only non-special characters that represent a sequence of characters. If ABC appears anywhere in the string, when we run a test, the test will return true.

### Sets of characters

Regular expressions enable us to describe complex patterns. If you want to match any digit in a regular expression, place a set of characters in-between square brackets. The following expressions match every string containing a digit:

```
console.log(/[0123456789]/.test("in 1992"));
// → true
console.log(/[0-9]/.test("in 1992"));
// → true
```

A hyphen (-) between two characters inside square brackets is used to specify a range of characters that the characters' Unicode numbers determine. Characters from 0 to 9 stay next to each other in this order (codes 48 to 57), so [0-9] covers all of them and matches any digit. Common character groups have built-in shortcuts. Digits are one such group: `\d` means the same thing as [0-9].

- `\d` Any digit character
- `\w` An alphanumeric character (“word character”)
- `\s` Any whitespace character (space, tabs, newline, and similar)
- `\D` A character that is not a digit
- `\W` A nonalphanumeric character
- `\S` A nonwhitespace character
- `.` Any character except newline

So, match a date and time format like 01-30-2003 15:20 with the expression below:

```
let dateTime = /\d\d-\d\d-\d\d\d\d \d\d:\d\d/;
console.log(dateTime.test("01-30-2003 15:20"));
// → true
console.log(dateTime.test("30-jan-2003 15:20"));
// → false
```

These backslash codes are also utilized within square brackets. For instance, `[\d.]` matches any digit or period character; the period has no special meaning, as do other special characters, like +.

```
let notBinary = /^[^01]*/;
console.log(notBinary.test("1100100010100110"));
// → false
console.log(notBinary.test("1100100010200110"));
// → true
```

### Repeating parts of a pattern

Now you have a good understanding of how to match single digits. If you want to match a whole number or a succession of more digits, place a plus sign (+) immediately after an element in a regular expression. This signifies that the element may repeat more than once; `/\d+/` matches one or more digit characters.

```
console.log(/\d+/.test("123"));
// → true
console.log(/\d+/.test(""));
// → false
console.log(/\d*/.test("123"));
// → true
console.log(/\d*/.test(""));
// → true
```

The star (*) enables the pattern to match zero occurrences. In the below example, the `u` character is permitted to appear, but the pattern also matches when it is not found.

```
let neighbor = /neighbour/;
console.log(neighbor.test("neighbour"));
// → true
console.log(neighbor.test("neighbor"));
// → true
```

To determine if a pattern element should occur a certain number of times, utilize the braces, inserting `{4}` after an element. If you want it to occur exactly four times, use `{4}`. A range like `{2,4}` signifies that the element must occur at least twice and at most four times. Below is another version of the date and time pattern, which enables both single and double-digit days, months and hours.

```
let dateTime = /\d{1,2}-\d{1,2}-\d{4} \d{1,2}:\d{2}/;
console.log(dateTime.test("01-30-2003 8:45"));
// → true
```

### Grouping subexpressions

If you want to utilize an operator like * or + on one or more elements at once, use parentheses. Parts of a regular expression enclosed in parentheses count as a single element as far as the operators are concerned.

```
let cartoonCrying = /boo+(hoo+)+/i;
console.log(cartoonCrying.test("Boohooohooohooo"));
// → true
```

The first and second + characters only apply to the second 'o' in 'boo' and 'hoo'. The third + applies to the entire group (hoo+), matching one or more occurrences of that group. The i at the end of the expression in the example is used for case insensitivity, enabling it to match the uppercase B in the input string, although the pattern is entirely lowercase.

### Matches and groups

The test method is the best way to test a regular expression; it determines only whether it matches. Regular expressions also have an exec (execute) method, which will return null if it could not find a match and return an object containing data about the match otherwise.

```
let match = /\d+/.exec("one two 100");
console.log(match);
// → ["100"]
console.log(match.index);
```
