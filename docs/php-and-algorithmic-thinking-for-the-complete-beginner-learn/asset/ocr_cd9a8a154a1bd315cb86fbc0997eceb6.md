# Conventions Used in This Book

Following are some explanations on the conventions used in this book. “Conventions” refer to the standard ways in which certain parts of the text are displayed.

# PHP Statements

This book uses plenty of examples written in PHP language. PHP statements are shown in a typeface that looks like this.

```
This is a PHP statement
```

# Keywords, Variables, Functions, and Arguments Within the Text of a Paragraph

Keywords, variables, functions, and arguments are sometimes shown within the text of a paragraph. When they are, the special text is shown in a typeface different from that of the rest of the paragraph. For instance, $first_name = 5 is an example of a PHP statement within the paragraph text.

# Words in Italics

You may notice that some of the special text is also displayed in italics. In this book, italicized words are general types that must be replaced with the specific name appropriate for your data. For example, the general form of a PHP statement may be presented as

```
echo arg1, arg2, arg3;
```

In order to complete the statement, the keywords arg1, arg2, and arg3 must be replaced with something meaningful. When you use this statement in your program, you might use it in the following form.

```
echo $a, $b, "Hello";
```

# Three dots (...): an Ellipsis

In the general form of a statement you may also notice three dots ( ... ), also known as an “ellipsis,” following a list in an example. They are not part of the statement. An ellipsis indicates that you can have as many items in the list as you want. For example, the ellipsis in the general form of the echo statement

```
echo arg1, arg2, ...;
```

indicates that the list may contain more than two arguments. When you use this statement in your program, your statement might be something like this.

```
echo $a, $b, $c, $d, $e;
```

# Square Brackets

The general form of some statements or functions may contain “square brackets” [], which indicate that the enclosed section is optional. For example, the general form of the statement

```
substr ( string , start [ , length ] )
```

indicates that the section [ , length] can be omitted.