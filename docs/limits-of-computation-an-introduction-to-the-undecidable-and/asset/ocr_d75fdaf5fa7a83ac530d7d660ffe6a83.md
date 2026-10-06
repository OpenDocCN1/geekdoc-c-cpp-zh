# Limits of Computation

There is no particular reason that a symbol has to be a connected line—consider the symbol j, or the symbol x. There is also no particular reason that a symbol has to have a well-defined name, except that then we would be reduced to making names for each one (squiggle-1, squiggle-2, etc.). Exotic, artistic alphabets are hard to name, and thus to discuss and to write. The standard alphabets in formal language theory consist of some set of standard characters, perhaps with embellishments such as x or x'. In most class and text examples, alphabets are small. The alphabets {0, 1} or {a, b, c} are used in many examples.

string over the alphabet Σ is a finite sequence of symbols from Σ.

Letters near the end of the alphabet are often used as names of strings (u, v, w, etc.). To stand for the symbols in the string, σ (or sometimes τ) will be used.

# Definition 2.3

The length of a string w, denoted |w|, is the number of nonunique characters w contains. As strings are finite, every string has a defined lengths.

# Examples

w = abb = σ₁σ₂σ₃ over Σ = {a, b, c}, σ₁ = a, σ₂ = σ₃ = b, |w| = |abb| = 3

u = bbbb over Σ = {a, b, c}, |u| = |bbbb| = 4

v = 1001111 over Σ = {0, 1}, |v| = 7

Note: Sequences have different notations—often the notation used depends on whether the sequence is used in a course in mathematics, for formal languages, or algorithms analysis.

```
w = ababa (formal languages)
w = (a, b, a, b, a) (algorithms analysis)
```