```
for (let arg of args) {
  value = evaluate(arg, scope);
}
return value;
};
```

To build bindings and set new values, you should build a form called define. It awaits a word as its first argument and an expression providing the value to set to that word as its second argument. Since define is an expression, it must send back a value. We will return the value that was set (like JavaScript’s = operator).

```
specialForms.define = (args, scope) => {
  if (args.length != 2 || args[0].type != "word") {
    throw new SyntaxError("Incorrect use of define");
  }
  let value = evaluate(args[1], scope);
  scope[args[0].name] = value;
  return value;
};
```

# The environment

The scope that evaluate allows is an object containing few properties that have their name tally with binding names. Their values are in accordance to the values those bounded bindings. Below is an illustration of an object to stand for global scope. To enable the utilization of the earlier described if construct, the Boolean values must be accessible. Therefore, there are two Boolean values only, all you need to do is to bind two names to the values true and false and utilize them.

```
const topScope = Object.create(null);
topScope.true = true;
topScope.false = false;
```

We can now examine a simple expression that nullify a Boolean value.

```
let prog = parse(`if(true, false, true)`);
console.log(examine(prog, topScope));
// → false
```

To provide fundamental arithmetic as well as comparison operators, lets include function values to scope. We will use function on few operator functions within a loop, and not stating them one by one.

```
for (let op of ["+", "-", "*", "/", "==", "<", ">"] ) {
  topScope[op] = Function("a, b", `return a ${op} b;`);
}
```

We will enclose console.log in a function to output the values