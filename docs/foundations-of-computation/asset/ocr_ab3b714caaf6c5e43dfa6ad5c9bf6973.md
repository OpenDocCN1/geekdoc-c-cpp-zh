derivation of $(x + y) * z + z * x$ must be $E \Longrightarrow E + T$. However, the first seven characters of the strings are identical, so clearly looking even seven characters ahead is not enough to tell us which production rule to apply. In fact, similar examples show that looking ahead any given finite number of characters is not enough.

However, there is an alternative parsing procedure that will work for $G_3$. This alternative method of parsing a string produces a **right derivation** of the string, that is, a derivation in which at each step, the non-terminal symbol that is replaced is the rightmost non-terminal symbol in the string. Here, for example, is a right derivation of the string $(x + y) * z$ according to the grammar $G_3$:

```
E \Longrightarrow T
\Longrightarrow T * F
\Longrightarrow T * z
\Longrightarrow F * z
\Longrightarrow (E) * z
\Longrightarrow (E + T) * z
\Longrightarrow (E + F) * z
\Longrightarrow (E + y) * z
\Longrightarrow (T + y) * z
\Longrightarrow (F + y) * z
\Longrightarrow (x + y) * z
```

The parsing method that produces this right derivation produces it from "bottom to top." That is, it begins with the string $(x + y) * z$ and works backward to the start symbol $E$, generating the steps of the right derivation in reverse order. The method works because $G_3$ is what is called an **LR(1) grammar**. That is, roughly, it is possible to read a string from **Left** to right and produce a **Right** derivation of the string, by looking ahead at most 1 symbol at each step. Although LL(1) grammars are easier for people to work with, LR(1) grammars turn out to be very suitable for machine processing, and they are used as the basis for the parsing process in many compilers.

LR(1) parsing uses a **shift/reduce** algorithm. Imagine a cursor or current position that moves through the string that is being parsed. We can visualize the cursor as a vertical bar, so for the string $(x + y) * z$, we start with the configuration $[(x + y) * z$. A **shift** operation simply moves the cursor one symbol to the right. For example, a shift operation would