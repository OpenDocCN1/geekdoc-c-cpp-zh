Note that `&` (like `|`, `~`, `>>`, and `<<`) delivers a set of bits. For example, if `a` and `b` are unsigned chars, `a&b` is an unsigned char with each bit being the result of applying `&` to the corresponding bits in `a` and `b`; see §A.5.5.

See §A.5.5.

For example:

```
`template<class T> T& max(T& a, T& b) { return (a>b)?a:b; }`
```

The “question mark colon operator” is explained in §8.4.

| **Bitwise and** |
| `x&y` | bitwise and of `x` and `y` |
| **Bitwise xor** |
| `x^y` | bitwise exclusive or of `x` and `y` |
| **Bitwise or** |
| `x|y` | bitwise or of `x` and `y` |
| **Logical and** |
| `x&&y` | logical and; returns `true` or `false`; evaluate `y` only if `x` is true |
| **Logical or** |
| `x||y` | logical or; returns `true` or `false`; evaluate `y` only if `x` is false |
| **Conditional expression** |
| `x?y:z` | if `x` the result is `y`; otherwise the result is `z.` |
| **Assignments** |
| `v=x` | assign `x` to `v`; result is the resulting `v` |
| `v*=x` | roughly `v=v*(x)` |