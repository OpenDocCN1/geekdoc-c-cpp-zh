![](bbox=[0.177, 0.095, 0.754, 0.192])

Figure 2-6  Syntax error for failing to use F suffix

The **double** type is used throughout the textbook for all numbers that require a fractional value.

# ## DECIMAL TYPES

The **decimal** value type is new to modern programming languages. It is appropriate for storing monetary data items because it allows both integral (whole) numbers and a fractional portion. It provides for greater precision than what is found with floating-point types because 128 bits are used to represent the value.

Numbers ranging from negative −79,228,162,514,264,337,593,543,950,335 to positive 79,228,162,514,264,337,593,543,950,335 can be stored in a **decimal** value type. As you can see in Table 2–11, 28 to 29 digits are possible with the **decimal**.

**Table 2-11**  Value and size for decimal data type

| Type | Numeric range | Precision | Size |
|---|---|---|---|
| `decimal` | 1.0 × 10^-28 to 7.9 × 10^28 | 28–29 significant digits | 128 bits |

As is the case with the **float** type, it is necessary to attach the suffix m or M onto the end of a number to indicate **decimal**, as shown in Example 2–6. Without the suffix, the number is treated as a **double**. Again, a syntax error message is issued if you try to do compile-time initialization or assign a number to a **decimal** variable without the suffix. No automatic conversion occurs.

# ### Example 2-6

```
```text
decimal endowmentAmount = 33897698.26M;
decimal deficit;
```
```