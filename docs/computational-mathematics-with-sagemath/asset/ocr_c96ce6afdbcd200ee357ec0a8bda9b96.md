e

To restore the original value, one can type for example:

```
```
sage: from sage.all import pi
```
```

or alternatively

```
```
sage: restore()
```
```

which restores to their default value *all* predefined variables and functions. The `reset()` function performs an even more complete reset, in particular it clears all user-defined variables.

# 1.2.5 Symbolic Variables

We have played so far with constant expressions like \(\sin(\sqrt{2})\), but Sage is especially useful in dealing with expressions containing variables like \(x + y + z\) or \(\sin(x) + \cos(x)\). The “mathematician's” *symbolic variables* \(x, y, z\) appearing in those expressions differ in general from the “programmer's” variables encountered in the preceding section. On this point, Sage differs notably from other computer algebra systems like Maple or Maxima.

The symbolic variables should be explicitly declared before being used² (SR abbreviates *Symbolic Ring*):

```
```
sage: z = SR.var('z')
sage: 2*z + 3
2*z + 3
```
```

In this example, the command `SR.var('z')` *builds* and returns a symbolic variable whose name is \(z\). This symbolic variable is a perfect Sage object: it is handled exactly like more complex expressions like \(\sin(x) + 1\). Then, this symbolic variable is assigned to the “programmer's” variable \(z\), which enables one to use it like any other expression, to build more complex expressions.

We could have assigned \(z\) to another variable than \(z\):

```
```
sage: y = SR.var('z')
sage: 2*y + 3
2*z + 3
```
```

Hence, assigning the symbolic variable \(z\) to the Python variable `z` is just a convention, which is however recommended to avoid confusion.

Conversely, the Python variable `z` does not interact with the symbolic variable \(z\):

```
```
sage: c = 2 * y + 3
sage: z = 1
sage: 2*y + 3
2*z + 3
sage: c
```
```

²Except the symbolic variable \(x\), which is predefined in Sage.