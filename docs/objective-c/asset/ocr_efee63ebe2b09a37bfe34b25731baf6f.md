of variables that you encounter include member variables, which are variables that are members of a class, and instance variables, which are variables that store a particular instance of an object. I cover both of these in Chapter 3 when I discuss objects.

When working with variables in Objective-C, they first must be declared, which means that you have to tell the compiler you’re going to use them. When you declare them, you have to give the type. There are three broad categories of types — scalars, pointers, and structures. It is these three categories that we talk about in the next sections.

# Using comments

Listings 2.4 and 2.5 introduced another bit of syntax, the double slash (//). In Objective-C, lines that are preceded by // are comments. They are ignored by the compiler, and can contain anything you want. Usually, they’re used to give some kind of human-readable documentation in the code, but they can just as often be used to temporarily remove code, or simply for the purposes of making the code pretty. The important thing to know is that whenever you see // in code, everything on that line until the end of that line will be ignored by the compiler.

In addition to the // style comments, there’s another syntax for comments delineated by the characters /* and */. In this case, rather than commenting everything to the end of the line, it only comments the text contained within the /* and */ characters.

Which of these commenting techniques you use is entirely up to you. I prefer the // style commenting, so that’s what I use throughout this book.

# Exploring scalar types

The first and most basic form of variable is scalar variables. A scalar is a type of value that can hold only one value at a time. Examples of scalars are integers, floating point numbers, and characters. Scalars have different defined sizes in terms of their memory footprint and the size of values that can be stored in them. You should be aware of these limitations when deciding what type to define your variables to be. Table 2.1 shows the size of the most commonly used scalar types in Objective-C.

| Table 2.1 Commonly used scalar types |
| Type | Description |
| int | An integer value between +/- 2,147,483,647. |
| unsigned int | An integer value between 0 and 4,294,967,296. |
| float | A floating point value between +/- 16,777,216. |
| double | A floating point value between +/- 2,147,483,647. |
| long | An integer value varying in size from 32 bit to 64 bit depending on architecture. |