# Languages ■ 15

The shortest string over any alphabet is the empty string—a string with no characters at all. We denote the empty string as $\varepsilon$—the Greek letter epsilon—although some authors use $\varepsilon$ or $\lambda$ instead. Its length is zero, $|\varepsilon| = 0$.

There is no longest string over an alphabet. A string may be of any length, so long as it is finite.

# Examples

Consider the two alphabets $\Sigma_1 = \{a, b, c\}$ and $\Sigma_2 = \{b, c, d\}$. The following- strings over both $\Sigma_1$ and $\Sigma_2$:

```
$\varepsilon$
bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
bbcbcb
```

The following are not strings over $\Sigma_1$ and $\Sigma_2$:

```
abacabad $(d \notin \Sigma_1, a \notin \Sigma_2)$nb b c (")”—that is, blank—$\Sigma_1$ or $\Sigma_2$)
```

An exponent can be used to note the **repetition** or number of times a character is repeated within a string.

# Example

```
$a^4b^5a^2 = aaaabbbbbaa
b^{28} = bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
0^5 = 00000
a^0 = \varepsilon
1^3 = 111$ (This is a string operation, not arithmetic!)
```

# Definition 2.4

A language over $\Sigma$ is a set of strings over $\Sigma$.