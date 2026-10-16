Even though I’ve defined a bunch of variables at the top of my `main()` function, you don’t have to declare all of your variables in one place. As you’ll see later in the program, I often define a new variable just before I use it.

# Naming Variables

To declare a variable, you must provide a name, known as an *identifier*. There are only a few rules you have to follow to create a legal identifier.

+   - An identifier can contain only numbers, letters, and underscores.
+   - An identifier can’t start with a number.
+   - An identifier can’t be a C++ keyword.

A *keyword* is a special word that C++ reserves for its own use. There aren’t many, but to see a full list, check out Appendix C.

In addition to the rules for creating *legal variable names*, following are some guidelines for creating *good variable names*.

+   - **Choose descriptive names.** Variable names should be clear to another programmer. For example, use `score` instead of `s`. (One exception to this rule involves variables used for a brief period. In that case, single-letter variable names, such as `x`, are fine.)
+   - **Be consistent.** There are different schools of thought about how to write multiword variable names. Is it `high_score` or `highScore`? In this book, I use the second style, where the initial letter of the second word (and any other words) is capitalized, known as *camel case*. But as long as you’re consistent, it’s not important which method you use.
+   - **Follow the traditions of the language.** Some naming conventions are just traditions. For example, in most languages (C++ included) variable names start with a lowercase letter. Another tradition is to avoid using an underscore as the first character of your variable names. Names that begin with an underscore can have special meaning.
+   - **Keep the length in check.** Even though `playerTwoBonusForRoundOne` is descriptive, it can make code hard to read. Plus, long names increase the risk of a typo. As a guideline, try to limit your variable names to fewer