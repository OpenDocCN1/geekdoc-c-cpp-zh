These are known as *comparison operators*. The comparison operators in C and, by extension, Arduino is like so:

s == t

This checks to see whether or not s and t are equal.

s < t

This checks to see whether or not s is less than t.

s <= t

This checks to see whether or not s is less than or equal to t.

s > t

This checks to see whether or not s is more than t.

s >= t

This checks to see whether or not s is either greater than or equal to t.

s != t

This checks to see whether or not s is *not equal* to t.

One of these comparisons has two names: a *statement* and an *expression*. In programming, they’re generally referred to as expressions in order to not confuse them with the computer science concept of the statement, but you can actually evaluate more than one of these expressions at once. This is known as *statement calculus*, and it occurs through the use of what are called *logical operators*.

There are many logical operators, but the ones in C that you most need to know are like so:

A && B

Checks to see if both expression A and expression B are true.