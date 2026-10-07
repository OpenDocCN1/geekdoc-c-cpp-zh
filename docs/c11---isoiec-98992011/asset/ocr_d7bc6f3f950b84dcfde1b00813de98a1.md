# ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – All rights reserved

# Semantics

A jump statement causes an unconditional jump to another place.

# 6.8.6.1 The goto statement

# Constraints

+   The identifier in a goto statement shall name a label located somewhere in the enclosing function. A goto statement shall not jump from outside the scope of an identifier having a variably modified type to inside the scope of that identifier.

# Semantics

+   A goto statement causes an unconditional jump to the statement prefixed by the named label in the enclosing function.

EXAMPLE 1 It is convenient to jump into the middle of a complicated set of statements. The following outline presents one possible approach to a problem based on these three assumptions:

+   1. The general initialization code accesses objects only visible to the current function.

+   2. The general initialization code is too large to warrant duplication.

+   3. The code to determine the next operation is at the head of the loop. (To allow it to be reached by continue statements, from example.)

```
/* */
goto first_time;
for (; ;) {
    // determine next operation
    /* */
    if (need to reinitialize) {
        // reinitialize-only code
        /* */
        first_time:
            // general initialization code
            /* */
        continue;
    }
    // handle other operations
    /* ... */
}
```