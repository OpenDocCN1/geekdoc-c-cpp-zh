Now let q = 3. Consider first the case p ≡ -1 (mod 12). Here the all-one vector extends to the all-one vector of length p + 1 and it is orthogonal to itself. By Lemma 6.2.4, -1 ∈ Np and (ii)(a) follows from Theorem 6.4.2. Now suppose that p ≡ 1 (mod 12). By Lemma 6.2.4, -1 ∈ Qp and by Theorem 6.4.3, C⊥1 = D2. In this case the all-one vector in D1 extends to Ĩ = 11+1 · (-1) in D̃1. This vector is not orthogonal to itself, but is orthogonal to ĨD = Ip+1, where Ip+1 is the all-one vector of length p + 1 and D is the diagonal matrix diag(1, 1, ..., 1, -1). This proves (ii)(b).

**Example 6.6.15** We describe the extensions of the QR codes discussed in Examples 6.6.7, 6.6.8, and 6.6.11. We give the extension of the generating idempotent of odd-like codes; from this one can form a basis of the extended codes using shifts of the generating idempotent extended in the same way (see Theorem 4.3.6).

+   - The extended coordinate of either generating idempotent of an odd-like binary QR code of length 23 is 1. These extended codes are each self-dual and doubly-even by Theorem 6.6.14. They are extended binary Golay codes.
+   - The extended coordinate of either generating idempotent of an odd-like QR code of length 11 over F3 is -1. The extended codes are each self-dual by Theorem 6.6.14 and are extended ternary Golay codes.
+   - The extended coordinate of either generating idempotent of an odd-like QR code of length 5 over F7 is 1. These extended codes are each Hermitian self-dual; they are also dual to each other under the ordinary inner product by Theorem 6.6.14. They are equivalent to the hexacode.

We are now ready to describe, in general, the extensions of the odd-like QR codes D1 and D2 of length p over Fq. We want them both to be extended in the same way whenever possible. Recall that we defined D̃ for an arbitrary odd-like duadic code D of length n using a solution γ of (6.11). As an odd-like QR code is obtained from its even-like subcode by adjoining the all-one vector 1, in order for either D̃1 to be self-dual or dual to D̃2, the extended vector Ĩ, which is 1 extended by some γ ∈ Fq, must be orthogonal to itself. This means that p + γ²p² = 0 or

1 + γ²p = 0, (6.12)

which is (6.11) with n = p. Suppose that C1 is the even-like subcode of D1. We know that either -1 ∈ No or -1 ∈ Qp, implying C1μ+1 = C2 or C1μ-1 = C1, respectively. By Theorems 6.4.2 or 6.4.3, these yield C̃⊥1 = D̃1 or C̃1 = D̃2, respectively. Therefore, whenever (6.12) is satisfied, if -1 ∈ Np, D̃ is self-dual for i = 1 and 2, and if -1 ∈ Qp, D̃1 and D̃2 are duals of each other. This proves the following, using Lemma 6.2.4.

**Theorem 6.6.16** Let D1 and D2 be the odd-like QR codes of length p over Fq, p an odd prime. Suppose that (6.12) is satisfied. Then if p ≡ -1 (mod 4), D̃i is self-dual for i = 1 and 2, and if p ≡ 1 (mod 4), D̃1 and D̃2 are duals of each other.

Thus we are interested in the cases where (6.12) has a solution γ in Fq. This is answered by the following. We only need the case where q is a square modulo p since we are assuming QR codes of length p over Fq exist.