# # Conventions Used in This Book

Following are some explanations on the conventions used in this book. “Conventions” refer to the standard ways in which certain parts of the text are displayed.

# ## C++ Statements

This book uses plenty of examples written in C++ language. C++ statements are shown in a typeface that looks like this.

```
`This is a C++ statement`
```

# ## Keywords, Variables, Functions, and Arguments Within the Text of a Paragraph

Keywords, variables, functions, and arguments are sometimes shown within the text of a paragraph. When they are, the special text is shown in a typeface different from that of the rest of the paragraph. For instance, `first_name = 5` is an example of a C++ statement within the paragraph text.

# ## Words in Italics

You may notice that some of the special text is also displayed in italics. In this book, italicized words are general types that must be replaced with the specific name appropriate for your data. For example, the general form of a C++ statement may be presented as

```
`void name ( type1 arg1, type2 arg2 )`
```

In order to complete the statement, the keywords *name*, *type1*, *arg1*, *type2*, and *arg2* must be replaced with something meaningful. When you use this statement in your program, you might use it in the following form.

```
`void display_rectangle ( int width, int height )`
```

# ## Three dots (...): an Ellipsis

In the general form of a statement you may also notice three dots ( ... ), also known as an “ellipsis,” following a list in an example. They are not part of the statement. An ellipsis indicates that you can have as many items in the list as you want. For example, the ellipsis in the general form of the statement

```
`display_messages ( arg1, arg2, ... )`
```

indicates that the list may contain more than two arguments. When you use this statement in your program, your statement might be something like this.

```
`display_messages ( message1, "Hello", message2, "Hi!" )`
```

# ## Square Brackets

The general form of some statements or functions may contain “square brackets” [ ], which indicate that the enclosed section is optional. For example, the general form of the statement

```
`str.substr ( beginIndex [, endIndex ] )`
```

indicates that the section [, endIndex] can be omitted.