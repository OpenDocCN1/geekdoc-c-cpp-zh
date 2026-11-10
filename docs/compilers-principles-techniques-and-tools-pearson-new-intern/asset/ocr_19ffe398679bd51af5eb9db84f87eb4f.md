# ### 3.3. SPECIFICATION OF TOKENS

# #### 3.3.4 Regular Definitions

For notational convenience, we may wish to give names to certain regular expressions and use those names in subsequent expressions, as if the names were themselves symbols. If $\Sigma$ is an alphabet of basic symbols, then a *regular definition* is a sequence of definitions of the form:

```
```text
  d₁   →   r₁
  d₂   →   r₂
        ...
  dₙ   →   rₙ
```
```

where:

+   1. Each $d_i$ is a new symbol, not in $\Sigma$ and not the same as any other of the $d$'s, and
+   2. Each $r_i$ is a regular expression over the alphabet $\Sigma \cup \{d_1, d_2, \dots, d_{i-1}\}$.

By restricting $r_i$ to $\Sigma$ and the previously defined $d$'s, we avoid recursive definitions, and we can construct a regular expression over $\Sigma$ alone, for each $r_i$. We do so by first replacing uses of $d_1$ in $r_2$ (which cannot use any of the $d$'s except for $d_1$), then replacing uses of $d_1$ and $d_2$ in $r_3$ by $r_1$ and (the substituted) $r_2$, and so on. Finally, in $r_n$ we replace each $d_i$, for $i = 1, 2, \dots, n - 1$, by the substituted version of $r_i$, each of which has only symbols of $\Sigma$.

**Example 3.5:** C identifiers are strings of letters, digits, and underscores. Here is a regular definition for the language of C identifiers. We shall conventionally use italics for the symbols defined in regular definitions.

```
```text
letter_   →   A | B | ... | Z | a | b | ... | z | _
digit     →   0 | 1 | ... | 9
id        →   letter_ ( letter_ | digit )*
```
```

$\square$

**Example 3.6:** Unsigned numbers (integer or floating point) are strings such as 5280, 0.01234, 6.336E4, or 1.89E-4. The regular definition

```
```text
      digit   →   0 | 1 | ... | 9
     digits   →   digit digit*
optionalFraction  →   . digits | ε
optionalExponent  →   ( E ( + | - | ε ) digits ) | ε
     number   →   digits optionalFraction optionalExponent
```
```

is a precise specification for this set of strings. That is, an *optionalFraction* is either a decimal point (dot) followed by one or more digits, or it is missing (the empty string). An *optionalExponent*, if not missing, is the letter E followed by an optional + or - sign, followed by one or more digits. Note that at least one digit must follow the dot, so *number* does not match 1., but does match 1.0.

$\square$