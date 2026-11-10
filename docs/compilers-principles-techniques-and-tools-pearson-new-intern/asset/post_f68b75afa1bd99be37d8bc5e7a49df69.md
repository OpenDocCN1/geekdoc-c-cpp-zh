
## Terms for Parts of Strings

The following string-related terms are commonly used:

- 1. A *prefix* of string *s* is any string obtained by removing zero or more symbols from the end of *s*. For example, **ban**, **banana**, and ε are prefixes of **banana**.
- 2. A *suffix* of string *s* is any string obtained by removing zero or more symbols from the beginning of *s*. For example, **nana**, **banana**, and ε are suffixes of **banana**.
- 3. A *substring* of *s* is obtained by deleting any prefix and any suffix from *s*. For instance, **banana**, **nan**, and ε are substrings of **banana**.
- 4. The *proper* prefixes, suffixes, and substrings of a string *s* are those prefixes, suffixes, and substrings, respectively, of *s* that are not ε and not equal to *s* itself.
- 5. A *subsequence* of *s* is any string formed by deleting zero or more not necessarily consecutive positions of *s*. For example, **baan** is a subsequence of **banana**.

If *x* and *y* are strings, then the *concatenation* of *x* and *y*, denoted *xy*, is the string formed by appending *y* to *x*. For example, if *x* = dog and *y* = house, then *xy* = doghouse. The empty string is the identity under concatenation; that is, for any string \(s\), ε\(s\) = \(s\)ε = \(s\).

If we think of concatenation as a product, we can define the “exponentiation” of strings as follows. Define \(s^0\) to be ε, and for all \(i > 0\), define \(s^i\) to be \(s^{i-1}s\). Since ε\(s\) = \(s\), it follows that \(s^1 = s\). Then \(s^2 = ss\), \(s^3 = sss\), and so on.

### 3.3.2 Operations on Languages

In lexical analysis, the most important operations on languages are union, concatenation, and closure, which are defined formally in Fig. 3.6. Union is the familiar operation on sets. The concatenation of languages is all strings formed by taking a string from the first language and a string from the second language, in all possible ways, and concatenating them. The (Kleene) closure of a language \(L\), denoted \(L^*\), is the set of strings you get by concatenating \(L\) zero or more times. Note that \(L^0\), the “concatenation of \(L\) zero times,” is defined to be {ε}, and inductively, \(L^i\) is \(L^{i-1}L\). Finally, the positive closure, denoted \(L^+\), is the same as the Kleene closure, but without the term \(L^0\). That is, ε will not be in \(L^+\) unless it is in \(L\) itself.

| OPERATION | DEFINITION AND NOTATION |
| --- | --- |
| *Union of L and M* | \(L \cup M = \{s \mid s \text{ is in } L \text{ or } s \text{ is in } M\}\) |
| *Concatenation of L and M* | \(LM = \{st \mid s \text{ is in } L \text{ and } t \text{ is in } M\}\) |
| *Kleene closure of L* | \(L^* = \cup_{i=0}^{\infty} L^i\) |
| *Positive closure of L* | \(L^+ = \cup_{i=1}^{\infty} L^i\) |

Figure 3.6: Definitions of operations on languages

**Example 3.3:** Let \(L\) be the set of letters \(\{\text{A},\text{B},\dots,\text{Z},\text{a},\text{b},\dots,\text{z}\}\) and let \(D\) be the set of digits \(\{\text{0},\text{1},\dots,\text{9}\}\). We may think of \(L\) and \(D\) in two, essentially equivalent, ways. One way is that \(L\) and \(D\) are, respectively, the alphabets of uppercase and lowercase letters and of digits. The second way is that \(L\) and \(D\) are languages, all of whose strings happen to be of length one. Here are some other languages that can be constructed from languages \(L\) and \(D\), using the operators of Fig. 3.6:

- 1. \(L \cup D\) is the set of letters and digits — strictly speaking the language with 62 strings of length one, each of which strings is either one letter or one digit.
- 2. \(LD\) is the set of 520 strings of length two, each consisting of one letter followed by one digit.
- 3. \(L^4\) is the set of all 4-letter strings.
- 4. \(L^*\) is the set of all strings of letters, including \(\epsilon\), the empty string.
- 5. \(L(L \cup D)^*\) is the set of all strings of letters and digits beginning with a letter.
- 6. \(D^+\) is the set of all strings of one or more digits.

□

### 3.3.3 Regular Expressions

Suppose we wanted to describe the set of valid C identifiers. It is almost exactly the language described in item (5) above; the only difference is that the underscore is included among the letters.

In Example 3.3, we were able to describe identifiers by giving names to sets of letters and digits and using the language operators union, concatenation, and closure. This process is so useful that a notation called *regular expressions* has come into common use for describing all the languages that can be built from these operators applied to the symbols of some alphabet. In this notation, if *letter* is established to stand for any letter or the underscore, and *digit* is

- c) `|` has lowest precedence and is left associative.

Under these conventions, for example, we may replace the regular expression `(a)|(b)*(c)` by `a|b*c`. Both expressions denote the set of strings that are either a single `a` or are zero or more `b`’s followed by one `c`.

**Example 3.4:** Let Σ = {a, b}.

- 1. The regular expression `a|b` denotes the language `{a, b}`.
- 2. `(a|b)(a|b)` denotes `{aa, ab, ba, bb}`, the language of all strings of length two over the alphabet Σ. Another regular expression for the same language is `aa|ab|ba|bb`.
- 3. `a*` denotes the language consisting of all strings of zero or more `a`’s, that is, `{ε, a, aa, aaa, …}`.
- 4. `(a|b)*` denotes the set of all strings consisting of zero or more instances of an `a` or `b`, that is, all strings of `a`’s and `b`’s: `{ε, a, b, aa, ab, ba, bb, aaa, …}`. Another regular expression for the same language is `(a|b)*`.
- 5. `a|a*b` denotes the language `{a, b, ab, aab, aaab, …}`, that is, the string `a` and all strings consisting of zero or more `a`’s and ending in `b`.

A language that can be defined by a regular expression is called a *regular set*. If two regular expressions r and s denote the same regular set, we say they are *equivalent* and write r = s. For instance, (a|b) = (b|a). There are a number of algebraic laws for regular expressions; each law asserts that expressions of two different forms are equivalent. Figure 3.7 shows some of the algebraic laws that hold for arbitrary regular expressions r, s, and t.

| LAW | DESCRIPTION |
| --- | --- |
| r&#124;s = s&#124;r | &#124; is commutative |
| r&#124;(s&#124;t) = (r&#124;s)&#124;t | &#124; is associative |
| r(st) = (rs)t | Concatenation is associative |
| r(s&#124;t) = rs&#124;rt; (s&#124;t)r = sr&#124;tr | Concatenation distributes over &#124; |
| εr = rε = r | ε is the identity for concatenation |
| r&#42; = (r&#124;ε)&#42; | ε is guaranteed in a closure |
| r&#42;&#42; = r&#42; | &#42; is idempotent |

Figure 3.7: Algebraic laws for regular expressions

## 3.3 SPECIFICATION OF TOKENS

### 3.3.4 Regular Definitions

For notational convenience, we may wish to give names to certain regular expressions and use those names in subsequent expressions, as if the names were themselves symbols. If $\Sigma$ is an alphabet of basic symbols, then a *regular definition* is a sequence of definitions of the form:

```text
  d₁   →   r₁
  d₂   →   r₂
        ...
  dₙ   →   rₙ
```

where:

- 1. Each $d_i$ is a new symbol, not in $\Sigma$ and not the same as any other of the $d$'s, and
- 2. Each $r_i$ is a regular expression over the alphabet $\Sigma \cup \{d_1, d_2, \dots, d_{i-1}\}$.

By restricting $r_i$ to $\Sigma$ and the previously defined $d$'s, we avoid recursive definitions, and we can construct a regular expression over $\Sigma$ alone, for each $r_i$. We do so by first replacing uses of $d_1$ in $r_2$ (which cannot use any of the $d$'s except for $d_1$), then replacing uses of $d_1$ and $d_2$ in $r_3$ by $r_1$ and (the substituted) $r_2$, and so on. Finally, in $r_n$ we replace each $d_i$, for $i = 1, 2, \dots, n - 1$, by the substituted version of $r_i$, each of which has only symbols of $\Sigma$.

**Example 3.5:** C identifiers are strings of letters, digits, and underscores. Here is a regular definition for the language of C identifiers. We shall conventionally use italics for the symbols defined in regular definitions.

```text
letter    →   A | B | ... | Z | a | b | ... | z | _
digit     →   0 | 1 | ... | 9
id        →   letter ( letter | digit )*
```

□

**Example 3.6:** Unsigned numbers (integer or floating point) are strings such as 5280, 0.01234, 6.336E4, or 1.89E-4. The regular definition

```text
      digit   →   0 | 1 | ... | 9
     digits   →   digit digit*
optionalFraction  →   . digits | ε
optionalExponent  →   ( E ( + | - | ε ) digits ) | ε
     number   →   digits optionalFraction optionalExponent
```

is a precise specification for this set of strings. That is, an *optionalFraction* is either a decimal point (dot) followed by one or more digits, or it is missing (the empty string). An *optionalExponent*, if not missing, is the letter E followed by an optional + or - sign, followed by one or more digits. Note that at least one digit must follow the dot, so *number* does not match 1., but does match 1.0.

□
