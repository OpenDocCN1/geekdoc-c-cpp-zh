# Tip - Value vs Reference

We have been using the term *value* throughout this book without precisely defining what exactly it is.

It is actually difficult to give a precise definition. A *value* is what the computer program deals with. Values can be stored in memory, e.g., during the execution of a program. A number *3* is a value, as well as a string "Hello".

When a function returns to the caller with a value, the value is copied, e.g., from one stack frame to another, or, more precisely, from the callee frame to the caller frame.

There are a special kind of values, namely, "references". A reference is special in that it "references" another value. Although it itself is a value (like number *3*, which can be copied, etc.), we do not mostly care about its own value in the program. We primarily care about the value that it references (or, "points to"). We often use the term "value" for non-reference values only. We use the terms *value* and *reference* almost mutually exclusively (although that is not entirely true).

Now, it is rather important to understand these concepts to be able to use C# more productively and effectively.

Sometimes, these concepts are tied to other related concepts like the stack memory and the heap memory. We will, however, mostly focus on the conceptual framework in this section rather than going over all the practical aspects. In theory, values and references can be stored in any kind of memory. The data that a reference points to, however, needs to be stored in a location in a "permanent", or at least "semi-permanent", memory (e.g., the heap).

A program construct, *variable*, can be used to store a value in a program. A variable has a "type". A type defines what kind of values a particular variable can have. And, what kind of operations are allowed on that variable, and so forth.

For example, a (mutable) variable of the `int` type can be used to store any valid 32