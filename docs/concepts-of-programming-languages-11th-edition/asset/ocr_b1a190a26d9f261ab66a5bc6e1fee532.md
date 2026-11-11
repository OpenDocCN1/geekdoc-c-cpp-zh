imperative features). It also makes testing easier, because each function can be tested separately, without any concern for its context.

A functional language provides a set of primitive functions, a set of functional forms to construct complex functions from those primitive functions, a function application operation, and some structure or structures for representing data. These structures are used to represent the parameters and values computed by functions. If a functional language is well designed, it requires only a relatively small number of primitive functions.

As we have seen in earlier chapters, the first functional programming language, Lisp, uses a syntactic form for both data and code that is very different from that of the imperative languages. However, many functional languages designed later use syntax for their code that is similar to that of the imperative languages.

Although there are a few purely functional languages, for example, Haskell, most of the languages that are called functional include some imperative features, for example, mutable variables and constructs that act as assignment statements.

Some concepts and constructs that originated in functional languages, such as lazy evaluation and anonymous subprograms, have now found their way into some languages that are considered imperative.

Although early functional languages were often implemented with interpreters, many programs written in functional programming languages are now compiled.

# 15.4 The First Functional Programming Language: Lisp

Many functional programming languages have been developed. The oldest and most widely used is Lisp (or one of its descendants), which was developed by John McCarthy at MIT in 1959. Studying functional languages through Lisp is somewhat akin to studying the imperative languages through Fortran: Lisp was the first functional language, but although it has steadily evolved for half a century, it no longer represents the latest design concepts for functional languages. In addition, with the exception of the first version, all Lisp dialects include imperative-language features, such as imperative-style variables, assignment statements, and iteration. (Imperative-style variables are used to name memory cells, whose values can change many times during program execution.) Despite this and their somewhat odd form, the descendants of the original Lisp represent well the fundamental concepts of functional programming and are therefore worthy of study.

# 15.4.1 Data Types and Structures

There were only two categories of data objects in the original Lisp: atoms and lists. List elements are pairs, where the first part is the data of the element, which is a pointer to either an atom or a nested list. The second part of a pair can be a pointer to an atom, a pointer to another element, or a special value, nil. Elements are linked together in lists with the second parts. Atoms and lists