# 24 ■ Limits of Computation

Complement (strings not in the language):

$L_2 = \{w \mid w \neq \varepsilon \text{ and } w \neq aa \text{ and } w \neq cba\}$

$L_4 = \{w \mid w \text{ does not contain exactly one }\}$

$L_6 = \Sigma^*$

But, because the elements of a language are strings, there are also other operations available.

# Definition 2.7

The concatenation of two languages $L_1$ and $L_2$ is the set of all strings that can be formed by concatenating a string from $L_1$, with a string from $L_2$.

$L_1L_2 = \{w \mid w = xy, x \in L_1 \text{ and } y \in L_2\}$

# Examples

Consider the following languages over $\{0, 1\}$:

+   $L_1 = {\varepsilon, 1, 00\}$

+   $L_2 = \{1, 11, 111\}$

+   $L_3 = \{w \mid w \text{ contains any number of } 0's \text{ (no } 1's); \text{ that is, } w = 0^k \text{ for some } k\}$

+   $L_4 = \{w \mid w \text{ contains any number of } 1's; \text{ i.e., } w = 1^j \text{ for some } j\}$

+   $L_5 = {\varepsilon\}$

+   $L_6 = \varnothing$

Then:

+   $L_1L_2 = \{1, 11, 001, 0011, 1111, 001111\}$