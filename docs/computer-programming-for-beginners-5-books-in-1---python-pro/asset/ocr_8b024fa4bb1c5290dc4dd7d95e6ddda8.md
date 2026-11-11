with another one.

```
console.log("papa".replace("p", "m"));
// → mapa
```

The first argument can equally be a regular expression. It replaces the first match of the regular expression. If you add a g option (for global) to the expression, every match contained in the string is replaced, and not first only.

```
console.log("Borobudur".replace(/[ou]/, "a"));
// → Barobudur
console.log("Borobudur".replace(/[ou]/g, "a"));
// → Barabadar
```

The major importance of utilizing regular expressions with replace is because it refers to matched groups in the replacement string. For instance, you have a large string consisting of people's name, one name per line, using the format Lastname, Firstname. You can as well change and remove these names, eradicate the comma to get a Firstname Lastname format, and utilize the following code:

```
console.log(
"Liskov, Barbara\nMcCarthy, John\nWadler, Philip"
.replace(/(\w+), (\w+)/g, "$2 $1"));
// → Barbara Liskov
// John McCarthy
// Philip Oaks
```

The $1 and $2 contained in the replacement string refer to the group in parentheses in pattern. $1 is restored by the text, which matches opposing the first group, $2 up to $9. Each and every match can be referred to with $&. You can pass a function instead of a string as the second argument to restore. For each replacement, the function is called with the matched group as arguments, and include the return value into the new string. Below is an example:

```
let s = "the cia and fbi";
console.log(s.replace(/\b(fbi|cia)\b/g,
str => str.toUpperCase()));
// → the CIA and FBI
```

Here’s a more interesting one:

```
let stock = "1 lemon, 2 cabbages, and 101 eggs";
function minusOne(match, amount, units) {
  amount = Number(amount) - 1;
  if (amount === 1) { // Just one left, remove the 's'
    unit = unit.slice(0, unit.length - 1);
  } else if (amount === 0) {
```