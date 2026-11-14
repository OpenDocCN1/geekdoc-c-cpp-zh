# # Advice

Always use `bool` for logical expressions.

Please note that comparisons cannot be chained like this:

Click here to view code image

```
bool in_bound= min <= x <= y <= max;    // Syntax error
```

Instead we need the more verbose logical reduction:

Click here to view code image

```
bool in_bound= min <= x && x <= y && y <= max;
```

In the following section, we will see similar operators.

# ## 1.3.3 Bitwise Operators

These operators allow us to test or manipulate single bits of integral types. They are important for system programming but less so for modern application development. Table 1–4 lists these operators by precedence.

The operation `x << y` shifts the bits of `x` to the left by `y` positions. Conversely, `x >> y` moves `x`'s bits `y` times to the right. In most cases, 0s are moved (except for negative `signed` values) to the right where they are implementation defined.

6. Again we compress the double less-than and larger-than symbols to French guillemets for nicer printing.

# ### Table 1–4: Bitwise Operators

| Operation | Expression |
|---|---|
| One's complement | ~x |
| Left shift | x << y |
| Right shift | x >> y |
| Bitwise AND | x & y |
| Bitwise exclusive OR | x ^ y |