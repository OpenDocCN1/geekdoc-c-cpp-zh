![](bbox=[0.11, 0.13, 0.195, 0.205])

Back in the old days of the C programming language, casting was a common way of converting data — *but it's actually somewhat dangerous*. In C, you could take any data type and directly cast it to any other data type. The idea was that if you wanted to burrow into the system and manipulate something (just about anything), you could. But over the years, people started to figure out that maybe, just *maybe*, this wasn't such a good idea. (As in, "Hey, bugs, welcome to my computer!") So although we're showing you how to cast, you should *try to avoid casting*. Instead, focus on converting (which sometimes uses castlike syntax) or using what are referred to as *safe casts*. See Chapter 9 in Book 1, as well as the next section ("Casting safely with C++") in this chapter, for details.

# ## Casting safely with C++

With the ANSI standard of C++ came all kinds of new goodies that make life easier than it used to be. Casting is one example. Originally, you could just cast all you wanted and change from one data type to another, possibly causing a mess, especially if you take existing code and compile it under a different operating system or perhaps even under a different compiler on the same operating system. One type may have a different underlying representation, and then, when you convert it on one system, you get one thing; take it to a different system and you get something else. That's bad. It creates bugs!

So the ANSI standard for C++ gives some newer and better ways of casting between items of data. These include `dynamic_cast` and `static_cast`.

# ## Dynamically casting with dynamic_cast

When the makers of C++ came up with these new ways of casting, their motivation was this: Think in terms of *conversions*. A cast simply takes one data type and tells the compiler to treat it as another data type. So first ask yourself if one of the conversions will work for you. If not, you can consider one of the new ways of casting.

# Book IV
Chapter 2

# Creating Data Structures

But remember, a *cast* tells the compiler to treat some data as another type of data. But the new ways of casting prevent you from doing a cast that doesn't make sense. For example, you may have a class hierarchy, and you have a pointer to a base class. But because an instance of a derived class can be treated as an instance of a base class, it's possible that this instance that you're looking at could actually be an instance of a derived class.

In the old style of C and C++ programming, you could just cast the instance and have at it:

```
`DoSomethingCool( (derivedClass *) someptr );`
```

In this case, we're assuming that someptr is of type pointer-to-base-class, but we're *hoping* that, in fact, it points to a derivedClass instance. Does it? It may, depending on how we wrote the rest of the application. But maybe