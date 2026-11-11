# Chapter 13: Parsing

Developing one's programming language is relatively easy and very exciting. This chapter will teach you how to build your language. We will create a programming language called Egg. A small, simple language is yet strong enough to express any thinkable computation. It enables pure abstraction determined functions.

# Parsing

The noticeable part of a programming language is the notation or syntax. A parser is a program that reads the text and provides a data layout that reflects the layout of the program within that text. If the text refuses to create a valid program, the parser would indicate an error. Our language would contain precise and uniform syntax. Everything included in Egg is an expression. An expression could be the binding name, number, string, or application. Utilize Applications for function calls and as well as constructs like if or while.

To keep the simple parser, strings within the Egg do not support backslash escapes. A string is a succession of characters that are not double quotes, enclosed in double-quotes. Name Binding can contain any character that isn't whitespace and that do not contain a unique meaning in the syntax. Write applications in JavaScript, by placing parentheses after an expression and putting any number of arguments within the parentheses, differentiated by commas.

```
do(define(x, 10),
if(>(x, 5),
  print("large"),
  print("small")))
```

The consistency of the Egg language means that operators in JavaScript (like the >) are called bindings in this language, utilized similarly like other functions. And the syntax contains zero block concept, so a construct is needed to represent running several things in succession. The data layout the parser utilizes to define a program containing expression objects. Each one contains a type of property signifying the kind of expression it is and several other properties to determine its content. Expressions of type "value" mean strings or numbers. Their value property consists of the string or number value that they stand for. Use expressions of type "word" for identifiers (names). These types of objects contain a name property that holds the identifier’s title as a string. And then the "apply" expressions stand for applications. They include an operator property that cites the applied expression, together with an args property that holds an array of argument expressions.

The >(x, 5) part of the new program would be like this: