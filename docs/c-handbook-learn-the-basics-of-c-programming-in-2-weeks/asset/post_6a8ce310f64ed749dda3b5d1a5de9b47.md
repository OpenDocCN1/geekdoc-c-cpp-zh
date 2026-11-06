
In this section, you'll learn about the non-symbol operators. To start the discussion, let's talk about an operator called “typeof.” This operator can help you in identifying the type of any value. Check the following examples:

```
console.log(typeof 4.5)
// → number
console.log(typeof "x")
// → string
```

The sample code given above used console.log to show the results you'll get with “typeof.” Whenever you run this kind of code, you should immediately see the value on your computer screen.

The operators given in the previous section required two values, while typeof requires one. Operators that require two values are known as binary operators. Those that work with a single value, however, are known as unary operators.

## The Boolean Values

Usually, programmers need values that can distinguish between two options, such as “on” or “off” and “yes” or “no.” For this purpose, the JavaScript language supports a value type called Boolean (which has two values only: true and false).

## Comparisons

You can use the following method to create Boolean values:

```
console.log(3 > 2)
// → true
console.log(3 < 2)
// → false
```

The < and > characters are the usual symbols used to represent “is less than” and “is greater than”, respectively. Both of these symbols fall under the “binary operators” category. If you'll apply them in your codes, you will get a Boolean value that shows whether they are true. You can compare strings using the same method.

```
console.log("Aardvark" < "Zoroaster")
// → true
```

Strings are ordered alphabetically. Also, lowercase letters are “more important” than uppercase ones. That means “a” > “b” is true. JavaScript also includes special characters (e.g. -, !, ?, etc.) in arranging strings. The process of comparison follows Unicode – it assigns a number to each character you might need in programming. This functionality is extremely useful since it allows you to store strings by converting them into number sequences. While comparing string values, JavaScript works from left to right, it checks the number sequences of each character individually.

You may also use similar operators such as <= (i.e. less than or equal to), >= (i.e. greater than or equal to), != (i.e. not equal to), and == (i.e. equal to). Check the following example:

```
console.log("Itchy" != "Scratchy")
// → true
```

In JavaScript, there is just one value that is unequal to itself. This value is NaN or “not a number.”

```
console.log(NaN == NaN)
// → false
```

Originally, NaN is used to represent the outcome of an irrational calculation. As such, it cannot be equal to the outcome of other irrational calculations.

## The Logical Operators

In this section, you'll learn about the different operations that you can apply to a Boolean value itself. The JavaScript language offers three operators, namely: and, not, and or. You can use these operators to perform logical processes on Boolean values. Because of that, they are known as “logical operators.”

### a) and

The && symbol represents “and.” This operator is binary. Additionally, it provides a “true” result ONLY IF the two values you are working on are both true. Here are some examples:

```
console.log(true && false)
// → false
console.log(true && true)
// → true
```

### b) or

You should use the “||” symbol to use if you want to use the “or” operator. “Or” will give you a “true” result if one of the values you are working on is true. Check the image below:

```
console.log(false || true)
// → true
console.log(false || false)
// → false
```

### c) not

You must use “!” (i.e. an exclamation mark) to indicate the “not” operator. This logical operator is unary: you can use it on a single value. However, “not” is unique in that it reverses the value you'll assign to it. For example, !false will give you true while !true will give you false.

## The Ternary Operator

This logical operator works on three different values. Known as the conditional operator, it requires you to use “?” and “:” in your scripts. The following code will show you how to use it:

```
console.log(true ? 1 : 2); // → 1
console.log(false ? 1 : 2); // → 2
```

The value placed on the left-hand side of the “?” determines which of the remaining values will be selected. If it is “true,” the first option is selected. If it is false, however, the second option is chosen.

## Undefined Values

The JavaScript language supports two special values to indicate the lack of a useful value. These special values are “undefined” and “null.” Although these two are considered as legitimate values, they don't carry any information.

Often, if a JavaScript operation cannot generate a useful value, it gives out “undefined” just because it is required to generate a value.

According to experts, the difference between null and undefined is a mistake on the part of JavaScript designers. That means these two values are considered equal most of the time. If you have to work on these values, just think of them as interchangeable elements in your scripts.

## How to Convert Types Automatically

You probably know that JavaScript accepts any application, even those that perform unusual things. The expressions listed below will demonstrate this concept clearly:

```
console.log(8 * null)
// → 0
console.log("5" - 1)
// → 4
console.log("5" + 1)
// → 51
console.log("five" * 2)
// → NaN
console.log(false == 0)
// → true
```

If you will apply an operator to an incorrect value type, JavaScript will automatically convert the said value into the proper type. JavaScript performs this function using a collection of rules that are sometimes unexpected or undesirable. Programmers refer to this automatic process as “type coercion.” Because of this, the null in the first line is converted to 0, while the “5” in the next line is converted to 5 (i.e. string-to-number conversion). The third line, however, tries to concatenate the values using the “+” sign, so the 1 becomes “1” (number-to-string-conversion).

If you'll convert a non-number value (“six” or undefined) into a number, you'll get NaN as a result. Applying mathematical operations on a NaN value will produce more NaNs, so if you are getting this value in unexpected or undesirable situations, check your codes for unwanted type conversions.

## Chapter 3: The Program Structure in JavaScript

This chapter will teach you “actual programming.” You'll be using JavaScript commands that go beyond the nouns and phrases you've used so far. Study this material carefully since it will help you master the basics of JavaScript in two weeks.

## Statements and Expressions

In the previous chapter, you generated new values by applying operators on existing values. It seems like value creation is the most important part of JavaScript programs. However, it's just a small part of this powerful language.

The part of a code that creates a value is known as “expression.” Thus, any value that you'll write literally (e.g. 99 or “ninety-nine”) falls under this category. Expressions are still called expressions even if you'll enclose them in parentheses. Also, an expression is still an expression even if you are using unary, binary, or ternary operators.

The paragraph above highlights the advantages of a programming interface that is based on language. Expressions act as subsentences in any human language – they can hold other expressions inside them. That means you can mix JavaScript expressions to state confusing calculations.

If expressions are equivalent to subsentences, JavaScript statements are equivalent to complete sentences. Basically, a JavaScript program is just a collection of statements.

The most basic type of statement is a value followed by a semicolon. Based on this principle, we can create this simple program:

```
0;
```

```
false;
```

In JavaScript, the sample given above is considered as a complete program. It's a worthless one, though. Statements are only useful if they do something that affects other things (e.g. showing some characters on the screen, improving the programming
