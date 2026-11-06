environment, etc.). The two statements shown above simply create two values (i.e. 0 and false). They don’t change or improve anything. If you’ll execute this program, you won’t observe anything significant.

# The Variables

How can JavaScript programs maintain themselves? How do they store things? You have seen how to create new values using old ones. However, that process doesn’t modify the preexisting values. You also need to use the resulting values immediately or they will simply disappear. To capture and hold values, JavaScript offers variables.

```
var example = 3 * 3;
```

In this example, var (one of the keywords in JavaScript) indicates that the line will create a variable. The keyword is followed by the variable’s name and, if you want to assign a value immediately, by an “ = ” sign and your desired expression.

The statement generates a variable named “ example ” and uses it to store the product of 3 * 3.

Once you have defined a variable, you can use its name as an ordinary expression in your future JavaScript statements. The value that you’ll get from that “ expression ” is identical to the value you assigned while creating it. Check the following example:

```
var three = 3;
console.log(three * three);
// -> 9
```

When naming variables, you can use any word that isn’t a keyword (e.g. var). You can include numbers in the variable’s name, but you can’t use a number as the initial character. For example, programming1 is valid but 1programming isn’t. Additionally, you cannot use spaces in naming variables. In terms of special characters, you can only use the dollar sign (i.e. $) and the underscore (i.e. _). JavaScript doesn’t allow you to use punctuation marks in variable names.

You may change the value assigned to a variable. In JavaScript, you can simply use the “ = ” sign on any variable to give it a new value.