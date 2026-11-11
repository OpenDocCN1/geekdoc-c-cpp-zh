```
amount = "no";
}
return amount + " " + units;
}
console.log(stock.replace(/(\d+) (\w+)/g, minusOne));
// → no lemon, 1 cabbage, and 100 eggs
```

# Greed

You can use replace to write a function that eradicates all comments from a block of JavaScript code. Look below:

```
function stripComments(code) {
  return code.replace(/\/\/.*|\/\*[^]*\*\//g, "");
}
console.log(stripComments("1 + /* 2 */3"));
// → 1 + 3
155
console.log(stripComments("x = 10; // ten!"));
// → x = 10;
console.log(stripComments("1 /* a */+/* b */ 1"));
// → 1 1
```

The section before the or operator matches two slash characters accompanied with any number that is not a newline character. Use [^] to match any character. Repetitive Operators (+, *, and {}) are called greedy which means they match and they can also backtrack. If a question mark is placed after them (+?, *?, ??, {}?), the greed disappears and begin matching no matter how small. The smallest stretch of characters which brings a */, is the star match. It absorbs one block comment only.

```
function stripComments(code) {
  return code.replace(/\/\*[\s\S]*?\*\/|\/\/.*?/g, "");
}
console.log(stripComments("1 /* a */+/* b */ 1"));
// → 1 + 1
```

# Dynamically creating RegExp objects

There are few instances whereby you would not understand the specific pattern you should match against when your code is being written. If you want to search for the user name in a chunk of text and wrap it in underscore characters to make it unique. But you can create a string and utilize the RegExp constructor. Below is an example: