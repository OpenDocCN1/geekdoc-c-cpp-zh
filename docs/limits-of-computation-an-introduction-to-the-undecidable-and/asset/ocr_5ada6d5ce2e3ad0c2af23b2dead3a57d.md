# Example

Let $\Gamma = \{B, 0, 1, 0', 1'\}$, the current state be $q_{273}$, $0011'010'11$ be the nonblank portion of the tape, and the read/write head positioned over the second nonblank symbol.

The configuration is written as $q_{273}$; $0011'010'11$.

An alternate representation (often found in other texts) that is shorter (but perhaps less readable) is to encode the current state directly into the tape contents. This style of representation shows where the read/write head is located by placing the current state immediately in front of the symbol beneath it.

The configuration is sometimes written as $0q_{273}$ $0011'010'11$.

This notation (with the state embedded into the string) has one advantage—it does not require the extra underline to show the location of the head. It is also more economical; the entire configuration is encoded in one string.

If the read/write head is positioned over a blank to the left or the right of the nonblank symbols on the tape, that blank must be shown:

+   - $\Gamma = \{B, 0, 1, 0', 1'\}$
The current state be $q_{273}$
0011'010'11$ be the nonblank portion of the tape
read/write head positioned two positions to the left of the nonblank portion of tape

$q_{273}BB0011'010'11$ or $q_{273}BB0011'010'11$

(underline notation) (embedded notation)

One point: It is always assumed that the machine starts in a proper configuration—so there is no need to check that the read/write head is actually over the first symbol, that there are no blanks embedded in the input string, that the symbols on the tape all come from $\Gamma$, and so forth.

# 4.5 TERMINOLOGY

A few basic definitions are needed to describe the behavior of a Turing machine on a particular input: