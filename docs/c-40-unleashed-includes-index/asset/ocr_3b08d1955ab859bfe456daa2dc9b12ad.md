# OPTIMIZATION?

Couldn't the compiler have optimized the preceding code to just the constant value 7? After all, none of the operands involved in the expression are known at compile time. Sure, in this case this would be completely safe to do (and in fact, some functional languages would), but in the general case, this is not safe.

The reason doesn't lie in the operands, but in the operators. As discussed later, operators can be overloaded so that custom types can define their own meaning for operators. If those operators do not behave as a pure function—that is, side effects can occur—it's not safe to change any of the runtime behavior.

In case of Int32 operands, it just happens the compiler can know all the behavior statically. But even that is a bit brittle in relation to arithmetic overflow behavior. We'll come back to that later in this chapter.

All in all, C# is an imperative language, and this kind of nontrivial compile-time evaluation is avoided. One exception is the use of literals: If you were to write 1 + 2 * 3 in your source code, it would get evaluated at compile time and substituted with an integer value 7.

The first couple of lines of IL are fairly straightforward; they just deal with assigning constant 32-bit integer values to our local variables a, b, and c:

```
IL_0000: nop
IL_0001: ldc.i4.1
IL_0002: stloc.0
IL_0003: ldc.i4.2
IL_0004: stloc.1
IL_0005: ldc.i4.3
IL_0006: stloc.2
```

However, we can already illustrate the essentials of the evaluation stack here. I've omitted the res variable from Figure 5.3, as well as the third assignment (for c).

![](bbox=[0.07, 0.95, 0.95, 0.98])

FIGURE 5.3 Evaluation stack transitions for assigning constants to variables.