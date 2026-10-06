# EXERCISES

+   1. Construct reasonable definitions for these new string operations. The result might be one string, or a set of strings (a language):

+   a. Permute(w) = w with its characters rearranged
b. Half(w) = w with half its characters removed.
c. First_half(w) = ?

Can these definitions be extended to languages? If so, how? And if L strings over Σ = {a, b} that begin with aa and end bb:

+   a. What is Permute (L)?nb. What is Half (L)?
f. What is First_half (L)?

+   2. Consider these three languages, and these three homomorphisms (Σ = {a, b, c}).

+   L₁ = strings that begin with aa and end with bb
L₂ = strings with an even number of a's
L₃ = strings that do not contain the substring bbb

+   h₁: a → bb, b → ab, c → cc
h₂: a → ε, b → abc, c → ε
h₃: a → b, b → c, c → aa

What is hⱼ(Lᵢ) for i = 1, 2, 3, and j = 1, 2, 3?

+   3.

+   a. Define a language L_{smaller-than-w}. If w = aabb, under your definition, what is L_{smaller-than-w}?

+   b. For strings r, s, v, w with r < s and v < w, prove or disprove:
i. rv < sw
ii. vR < w^R