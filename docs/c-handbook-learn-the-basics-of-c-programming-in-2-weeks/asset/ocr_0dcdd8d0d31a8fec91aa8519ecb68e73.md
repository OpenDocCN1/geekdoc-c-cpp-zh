```
var taste = “ bitter ”;
console.log(taste);
// -> bitter
taste = “ sweet ”;
console.log(taste);
// -> sweet
```

In general, you should think of variables as tentacles instead of containers. A variable grasps values, it doesn ’ t contain them. That means multiple variables can point to a single value.

Let ’ s analyze a simple example. You need to generate a variable to remember the amount Johnny owes you. When he pays you $50, you have to assign a new value to the existing variable. Check the lines below:

```
var JohnnysDebt = 200;
JohnnysDebt = JohnnysDebt - 50;
console.log(JohnnysDebt);
// -> 150
```

If you will create a variable without assigning a value, it will be considered empty. It will give you “ undefined ” if you ’ ll ask for the value it contains.

JavaScript allows you to include several variables in one var statement. When using this functionality, you should separate the variables using commas. Here ’ s an example:

```
var three = 3, four = 4;
console.log(three + four);
// -> 7
```