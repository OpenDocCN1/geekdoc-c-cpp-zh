As an example, the current Scala compiler focuses on *tail recursive functions*—functions with a single recursive call, in tail position. It does not optimize other tail calls, including those inside mutually recursive functions. Furthermore, because functions are implemented as methods, and methods can be overridden, code that appears to be tail recursive may not be optimized. You can use a `tailrec` annotation to confirm that the optimization is indeed taking place: A function annotated with `tailrec` is guaranteed to be optimized by the compiler, or compilation will fail.

# Aside on Optimized Bytecode for Tail Recursive Functions

As an experiment, consider the small class shown here, with a single recursive method:

```
class TailRecursionTest:
  def zero(x: Int): 0 = if x == 0 then 0 else zero(x - 1)
```

The useless method always returns zero (hence its name and return type). The bytecode generated for it by the Scala compiler looks something like this:

```
public int zero(int);
Code:
  0: iload 1
  1: iconst_0
  2: if_icmpne 9
  5: iconst_0
  6: goto 16
  9: aload 0
 10: iload 1
 11: iconst_1
 12: isub
 13: invokevirtual #16    // Method zero:(I)I
 16: ireturn
```

The details are unimportant. Line 2 is a comparison of variable x with 0. If x is non-zero, execution jumps to line 9. Lines 9–12 calculate x − 1, and line 13 invokes method zero again, on x − 1. No optimization is taking place. If the method is annotated with tailrec, compilation will fail.

What prevents the compiler from optimizing is the fact that method zero could be overridden in a class that extends TailRecursionTest. If overriding is