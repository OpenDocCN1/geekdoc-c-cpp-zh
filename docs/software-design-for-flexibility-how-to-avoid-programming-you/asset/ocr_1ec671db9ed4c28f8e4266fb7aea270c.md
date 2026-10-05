attention to the appearance of new-dictionary in the body of match:list. This control structure, in essence, decrees that the leftmost, deepest instance of each unique pattern variable is a defining instance in an implicit flat global namespace, with all subsequent downstream appearances being constraining instances.

So let's not worry about scoping complexity in this exercise. Specifically, just as pattern variables all share a common global namespace, so too can your pattern definitions.

If you are really ambitious, you can implement lexical scoping by rewriting all the existing matcher interfaces to accept an extra pattern-environment parameter. But that is a job for another time and place (in exercise 4.9).

# Exercise 4.8: Hoist by our own petard

On the surface it may appear that it would be easy to extend this matcher system to allow vector patterns and vector data. But we made a strong assumption in the design of this matcher—that it is a matcher of list patterns on list data.

+   a. What would it take to liberate this code from that assumption so that you could make a matcher that encompassed both kinds of compound data? Or arbitrary sequences? What sorts of changes are required? Do you need to change the interface to a match procedure?

+   b. Make it so! (This is lots of work).

# Exercise 4.9: General pattern language

Even with the addition of ?:pletrec and ?:ref in exercise 4.7, the pattern matcher we have is not a complete language, in that it does not support namespace scoping and parametric patterns. For example, we cannot write the following pattern, which is intended to match only lists of symbols that are palindromes.