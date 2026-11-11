In addition, you can specify flags that control the appearance of the formatted output. Table 3.6 shows all flags. For example, the comma flag adds group separators. That is,

```
System.out.printf("%,.2f", 10000.0 / 3.0);
```

prints

```
3,333.33
```

You can use multiple flags, for example "%,(.2f" to use group separators and enclose negative numbers in parentheses.

**Table 3.6** Flags for `printf`

| Flag | Purpose | Example |
|---|---|---|
| `+` | Prints sign for positive and negative numbers. | `+3333.33` |
| `space` | Adds a space before positive numbers. | ` 3333.33` |
| `0` | Adds leading zeroes. | `0003333.33` |
| `-` | Left-justifies field. | `|3333.33  |` |
| `(` | Encloses negative numbers in parentheses. | `(3333.33)` |
| `,` | Adds group separators. | `3,333.33` |
| `# (for f format)` | Always includes a decimal point. | `3,333.` |
| `# (for x or o format)` | Adds `0x` or `0` prefix. | `0xcafe` |
| `$` | Specifies the index of the argument to be formatted; for example, `%1$d %1$x` prints the first argument in decimal and hexadecimal. | `159 9F` |
| `<` | Formats the same value as the previous specification; for example, `%<x` prints the same number in decimal and hexadecimal. | `159 9F` |

> **NOTE:** You can use the `s` conversion to format arbitrary objects. If an arbitrary object implements the `Formattable` interface, the object’s `formatTo` method is invoked. Otherwise, the `toString` method is invoked to turn the object into a string. We discuss the `toString` method in Chapter 5 and interfaces in Chapter 6.

You can use the static `String.format` method to create a formatted string without printing it: