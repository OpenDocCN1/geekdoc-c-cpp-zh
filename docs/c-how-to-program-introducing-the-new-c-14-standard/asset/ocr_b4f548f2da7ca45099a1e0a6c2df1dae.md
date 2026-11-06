# Observation 6.3

> > *Always provide function prototypes, even though it’s possible to omit them when functions are defined before they’re used. Providing the prototypes avoids tying the code to the order in which functions are defined (which can easily change as a program evolves).*

# 6.5.1 Function Signatures and Function Prototypes

The portion of a function prototype that includes the *name of the function* and the *types of its arguments* is called the **function signature** or simply the **signature**. The function’s return type is not part of the function signature. The scope of a function is the region of a program in which the function is known and accessible. *Functions in the same scope must have unique signatures.* We’ll say more about scope in [Section 6.10](#).

In [Fig. 6.3](#), if the function prototype in line 7 had been written

```
```
```