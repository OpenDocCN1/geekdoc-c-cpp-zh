constructor. Initialization lists just would not do the trick: I would directly set everything to zero in one assembly instruction.

You can imagine how I felt about assignment operators and copy constructors. Why weren’t they calling memcpy? What was it with this delicate, dainty, member-by-member stuff? I could understand in those cases where I actually had something to do during the constructor body, but when I was simply setting aside an area of memory, why was there such wastage?

I struggled through, cursing these inefficiencies, and trading them against the more intelligible code the other features were yielding. Sometimes I would write the truly performance-critical parts in C and exploit the fact that both languages were mutually intelligible to the linker.

The chimera is a mythical fire-breathing beast with the head of a lion, the body of a goat, and the tail of a dragon. I was writing these ghastly code chimeras in the 1990s. It took me a long time to realize that the error I was making was in declaring my objects too early in the function before they were ready to be used. In addition, this was prior to standardization and the introduction of the as-if rule. It took me even longer to realize the true value of that fine piece of legislation. Let’s look a little closer at the rules about construction.

The standard describes initialization of classes over 12 pages of standardese, starting at [class.init],¹ referring a further eight pages at [dcl.init]² if there is no con-structor. This really isn’t the place to parse all that, so we’ll keep things simple and summarize, starting with aggregates.

1. https://eel.is/c++draft/class.init
2. https://eel.is/c++draft/dcl.init

# The simplest possible class

Aggregates are classes with

+   - No user-declared or inherited constructors
+   - No nonpublic data members which are not static