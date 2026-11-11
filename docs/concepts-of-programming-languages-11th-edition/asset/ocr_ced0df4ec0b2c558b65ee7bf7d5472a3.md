# 6.9 List Types

Lists were first supported in the first functional programming language, Lisp. They have always been part of the functional languages, but in recent years they have found their way into some imperative languages.

Lists in Scheme and Common Lisp are delimited by parentheses and the elements are not separated by any punctuation. For example,

```
```lisp
(A B C D)
```
```

Nested lists have the same form, so we could have

```
```lisp
(A (B C) D)
```
```

In this list, (B C) is a list nested inside the outer list.

Data and code have the same syntactic form in Lisp and its descendants. If the list (A B C) is interpreted as code, it is a call to the function A with parameters B and C.

The fundamental list operations in Scheme are two functions that take lists apart and two that build lists. The CAR function returns the first element of its list parameter. For example, consider the following example:

```
```lisp
(CAR '(A B C))
```
```

The quote before the parameter list is to prevent the interpreter from considering the list a call to the A function with the parameters B and C, in which case it would interpret it. This call to CAR returns A.

The CDR function returns its parameter list minus its first element. For example, consider the following example:

```
```lisp
(CDR '(A B C))
```
```

This function call returns the list (B C).

Common Lisp also has the functions FIRST (same as CAR), SECOND, ..., TENTH, which return the element of their list parameters that is specified by their names.

In Scheme and Common Lisp, new lists are constructed with the CONS and LIST functions. The CONS function takes two parameters and returns a new list with its first parameter as the first element and its second parameter as the remainder of that list. For example, consider the following:

```
```lisp
(CONS 'A '(B C))
```
```

This call returns the new list (A B C).

The LIST function takes any number of parameters and returns a new list with the parameters as its elements. For example, consider the following call to LIST:

```
```lisp
(LIST 'A 'B '(C D))
```
```