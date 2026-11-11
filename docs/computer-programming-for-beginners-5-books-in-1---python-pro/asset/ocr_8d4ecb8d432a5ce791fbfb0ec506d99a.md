```
let name = "harry";
let text = "Harry is a suspicious character.";
let regexp = new RegExp("\\b(" + name + ")\\b", "gi");
console.log(text.replace(regexp, "_$1_"));
// → _Harry_ is a suspicious character.
```

If you want to build the \b boundary markers, utilize the two backslashes because you would write them in a normal string. The second argument to the RegExp constructor consists of the options needed for the regular expression. The "gi" represent global and case insensitive. Below is an example:

```
let name = "dea+hl[|]rd";
let text = "This dea+hl[|]rd guy is super annoying.";
let escaped = name.replace(/[\.\[.+*?{}()|^$]/g, "\\$&");
let regexp = new RegExp("\\b" + escaped + "\\b", "gi");
console.log(text.replace(regexp, "_$&_"));
// → This _dea+hl[|]rd_ guy is very annoying.
```

# The search method

You cannot call the indexOf method on strings a regular expression. You can also use another method, search whereby you can call the indexOf method a regular expression, and it sends back the first index where it sees the expression and when it does not see it returns -1.

```
console.log(" word".search(/\S/));
// → 2
console.log("".search(/\S/));
// → -1
```

# The lastIndex property

The exec method does not produce a better way to begin the search from a stated position in the string. Regular expression objects contain properties. One of the properties is called source, and it consists of the string that built the expression. lastIndex is another property, and it influences some small circumstances, where the next match will begin. The regular expression must contain the global (g) or sticky (y) option, and the match will occur using the exec method. Illustration below:

```
let pattern = /y/g;
pattern.lastIndex = 3;
let match = pattern.exec("xyzyy");
console.log(match.index);
// → 4
console.log(pattern.lastIndex);
```