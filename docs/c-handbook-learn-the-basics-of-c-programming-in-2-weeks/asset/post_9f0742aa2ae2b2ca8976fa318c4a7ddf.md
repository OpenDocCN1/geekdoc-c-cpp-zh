
environment, etc.). The two statements shown above simply create two values (i.e. 0 and false). They don't change or improve anything. If you'll execute this program, you won't observe anything significant.

## The Variables

How can JavaScript programs maintain themselves? How do they store things? You have seen how to create new values using old ones. However, that process doesn't modify the preexisting values. You also need to use the resulting values immediately or they will simply disappear. To capture and hold values, JavaScript offers variables.

```
var example = 3 * 3;
```

In this example, var (one of the keywords in JavaScript) indicates that the line will create a variable. The keyword is followed by the variable's name and, if you want to assign a value immediately, by an " = " sign and your desired expression.

The statement generates a variable named " example " and uses it to store the product of 3 * 3.

Once you have defined a variable, you can use its name as an ordinary expression in your future JavaScript statements. The value that you'll get from that " expression " is identical to the value you assigned while creating it. Check the following example:

```
var three = 3;
console.log(three * three);
// -> 9
```

When naming variables, you can use any word that isn't a keyword (e.g. var). You can include numbers in the variable's name, but you can't use a number as the initial character. For example, programming1 is valid but 1programming isn't. Additionally, you cannot use spaces in naming variables. In terms of special characters, you can only use the dollar sign (i.e. $) and the underscore (i.e. _). JavaScript doesn't allow you to use punctuation marks in variable names.

You may change the value assigned to a variable. In JavaScript, you can simply use the " = " sign on any variable to give it a new value.

```
var taste = "bitter";
console.log(taste);
// -> bitter
taste = "sweet";
console.log(taste);
// -> sweet
```

In general, you should think of variables as tentacles instead of containers. A variable grasps values, it doesn't contain them. That means multiple variables can point to a single value.

Let's analyze a simple example. You need to generate a variable to remember the amount Johnny owes you. When he pays you $50, you have to assign a new value to the existing variable. Check the lines below:

```
var JohnnysDebt = 200;
JohnnysDebt = JohnnysDebt - 50;
console.log(JohnnysDebt);
// -> 150
```

If you will create a variable without assigning a value, it will be considered empty. It will give you " undefined " if you'll ask for the value it contains.

JavaScript allows you to include several variables in one var statement. When using this functionality, you should separate the variables using commas. Here's an example:

```
var three = 3, four = 4;
console.log(three + four);
// -> 7
```

## The Reserved Words in JavaScript

As discussed earlier, you can't use keywords when naming your variables. However, there are other words that you can't use as variable names because JavaScript has reserved them for future developments. Here are some of the reserved words in this scripting language:

- in, do, let, if, new, try, with, case, void, with, while, false, yield, extends, delete, default, const, debugger, class, break, finally, null, private, return, import, protected, switch, super, interface, instanceof, throw, implements

Keep in mind that you can't use the words given above when defining variables. If you'll forget about this simple rule, you might experience problems when working with JavaScript programs.

## JavaScript Environments

The term "environment" refers to the set of active values and variables. Basically, environments cannot be empty while starting up a JavaScript program. Environments hold variables related to the language itself, and often, they have variables that allow interactions with computer systems. For instance, in web browsers, various functions and variables exist to check and affect the current website and read the inputs from the mouse and keyboard.

## The Functions

The default JavaScript environment involves functions. Functions are pieces of computer programs linked to a value. You may apply these values to activate the linked program. For instance, in browser environments, alert (i.e. a variable) contains a function that displays a dialog box. Here's an example:

```
alert( "You are not authorized to access this page!" );
```

You may execute a function by placing parentheses after a JavaScript expression that generates a function value. Often, you'll indicate the name of the variables that contain your desired functions. By enclosing values inside the parentheses, you are assigning those values to the program/s within the function. For the previous example, "alert" uses the assigned string to show a message in the resulting dialog box. Programmers use the term "arguments" when referring to the value/s assigned to a function.

## The "console.log"

You can use "alert" when trying out new strings or statements. However, since it requires you to close out the resulting windows, you might find it inconvenient and time-consuming. Because of this, you might want to use the function you've seen in the earlier sections of this book: console.log. Almost all JavaScript systems (e.g. Node.js, web browsers, etc.) offer this function to transfer arguments to a text-compatible output device.

When it comes to web browsers, the code's output goes to the console of JavaScript. Although this section of the browser GUI is usually hidden, you can access it by pressing certain keys (i.e. for Windows computers, hit F12; For Mac computers, hit Command-Option-I). If you are having problems viewing this part, you may run an intra-device search for "developer tools" or "web console." Analyze the following example:

```
var a = 99;

console.log("one hundred minus one is", a);

// -> one hundred minus one is 99
```

As discussed earlier, you can't use periods or commas when naming variables. However, the example given above contains one. The reason for this is that console.log isn't an ordinary variable. It is a JavaScript expression that collects the "log" information from the value stored in "console" (which is a variable).

## The Return Values

Writing information on the screen and displaying dialog boxes are known as side effects. Because of these side effects, functions are important in the JavaScript language. You may also use functions to generate values – in this case, a function can be useful even without its side effects. For instance, Math.max (a JavaScript function) receives an unlimited number of numeric values and indicates the highest one. Here's an example:

```
console.log(Math.max(1, 2, 3, 4, 5));
// -> 5
```

In JavaScript, anything that generates values is considered as an expression. That means you can perform function calls in large expressions. In the example below, you'll use the Math.min function as an input for the " + " operator:

```
console.log(Math.min(1, 2) + 98);
// -> 99
```

## Chapter 4: More Information About Functions in JavaScript

In the previous section, you've learned how to create and call function values. This chapter will help you understand this important topic further. According to expert programmers, functions serve as your main tools when using JavaScript. Functions are powerful tools that can help you design large programs, minimize redundancy, name subprograms, and secure isolation for each subprogram. That means you have to master functions if you want to use JavaScript effectively. This chapter will help you to learn this scripting language in just two weeks.

Many people apply functions to define new vocabularies. That means you can use them to create words and assign meanings.

An average English speaker has about 20,000 words in his/her vocabulary. Well, programming languages usually don't have that amount of built-in commands. That means the vocabulary in programming is more precise than those used in human languages. If you want to minimize redundancy, you have to add your own words into JavaScript and create your own vocabulary.
