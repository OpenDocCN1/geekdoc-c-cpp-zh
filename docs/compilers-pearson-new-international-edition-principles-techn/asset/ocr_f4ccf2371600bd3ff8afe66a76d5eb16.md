# 3.3. SPECIFICATION OF TOKENS

established to stand for any digit, then we could describe the language of C identifiers by:

letter_ ( letter_ | digit )*

The vertical bar above means union, the parentheses are used to group subexpressions, the star means “zero or more occurrences of,” and the juxtaposition of letter_ with the remainder of the expression signifies concatenation.

The regular expressions are built recursively out of smaller regular expressions, using the rules described below. Each regular expression r denotes a language L(r), which is also defined recursively from the languages denoted by r’s subexpressions. Here are the rules that define the regular expressions over some alphabet Σ and the languages that those expressions denote.

**BASIS:** There are two rules that form the basis:

+   1. ε is a regular expression, and L(ε) is {ε}, that is, the language whose sole member is the empty string.
+   2. If a is a symbol in Σ, then a is a regular expression, and L(a) = {a}, that is, the language with one string, of length one, with a in its one position. Note that by convention, we use italics for symbols, and boldface for their corresponding regular expression.¹

**INDUCTION:** There are four parts to the induction whereby larger regular expressions are built from smaller ones. Suppose r and s are regular expressions denoting languages L(r) and L(s), respectively.

+   1. (r)|(s) is a regular expression denoting the language L(r) ∪ L(s).
+   2. (r)(s) is a regular expression denoting the language L(r)L(s).
+   3. (r)* is a regular expression denoting (L(r))*.
+   4. (r) is a regular expression denoting L(r). This last rule says that we can add additional pairs of parentheses around expressions without changing the language they denote.

As defined, regular expressions often contain unnecessary pairs of parentheses. We may drop certain pairs of parentheses if we adopt the conventions that:

+   a) The unary operator * has highest precedence and is left associative.
+   b) Concatenation has second highest precedence and is left associative.

¹However, when talking about specific characters from the ASCII character set, we shall generally use teletype font for both the character and its regular expression.