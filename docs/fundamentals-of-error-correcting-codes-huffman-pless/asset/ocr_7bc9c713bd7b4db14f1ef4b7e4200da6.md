if p ≡ 5 (mod 12), and
1 + ρ Σ_{j∈Q_p} x^j + ρ^3 Σ_{j∈N_p} x^j   and   1 + ρ^3 Σ_{j∈Q_p} x^j + ρ Σ_{j∈N_p} x^j.
if p ≡ -5 (mod 12).

Proof: Part (i) follows from Theorem 6.6.4. Let e(x) be a generating idempotent for an even-like QR code C1 over Fp of length p with p ≡ ±5 (mod 12). Then by Theorem 6.6.3, e(x) = a0 + a1Q(x) + a2N(x), where ai ∈ Fq for 0 ≤ i ≤ 2. Using Lemma 6.6.1, notice that Q(x)^3 = Q(x^3) = N(x) and N(x)^3 = N(x^3) = Q(x) as 3 ∈ Np by Lemma 6.2.9. As e(x)^3 = e(x), we must have e(x)^3 = e(x). Thus e(x)^3 = a0^3 + a1^3N(x) + a2^3Q(x) + a2^3Q(x) = e(x), implying a0^3 = a0 and a2 = a1^3. The other even-like QR code C2 paired with C1 has generating idempotent e(x)μb, where b ∈ Np by Theorem 6.6.4. Again by Lemma 6.6.1, Q(x)μb = Q(x^b) = N(x) and N(x)μb = N(x^b) = Q(x). Therefore, e(x) = a0 + a1Q(x) + a1^3N(x) and e(x)μb = a0 + a1^3Q(x) + a1N(x).

We first consider the case p ≡ 5 (mod 12). By Theorem 6.6.6(ii),

e(x) + e(x)μb = -1 + x + x^2 + ... + x^{p-1}.

implying that 2a0 = -1 and a1 = 1. Thus a0 = 1; by examining Table 6.4, either a1 = -1 or ai ∈ {ρ, ρ^3}. As 1 - Q(x) - N(x) = -(-J(x)) generates Ep, a1 = -1 is impossible. So the two possibilities remaining for a1 must lead to generating idempotents for the two even-like QR codes that we know exist. The generating idempotents for the odd-like codes follow from Theorem 6.6.4.

We leave the case p ≡ -5 (mod 12) as an exercise. □

Exercise 366 Prove Theorem 6.6.12 in the case p ≡ -5 (mod 12). ◆

The following theorem is analogous to Theorem 6.6.9 and is proved in the same way.

# Theorem 6.6.13 Let p be an odd prime with p ≠ 3. The following hold:

+   (i) Quadratic residue codes of length p over F3, where t is odd, exist if and only if p ≡ ±1 (mod 12), and the generating idempotents are those given in Theorem 6.6.10.
+   (ii) Quadratic residue codes of length p over F7, where t is even, exist for all p, and the generating idempotents are those given in Theorems 6.6.10 and 6.6.12.

Exercise 367 Give the generating idempotents for all quadratic residue codes of prime length p ≤ 29 over F7. Distinguish between the idempotents that generate even-like codes and those that generate odd-like codes. Also distinguish between those that arise when t is even and when t is odd. ◆

+   Exercise 368 Let D1 and D2 be odd-like quadratic residue codes of prime length p ≠ 3 over Fq with even-like subcodes C1 and C2. Prove the following:
+   (a) If p ≡ -1 (mod 12), then C1 and C2 are self-orthogonal.
+   (b) If p ≡ 1 (mod 12), then C1^⊥ = D2 and C2^⊥ = D1.
+   (c) If p ≡ -5 (mod 12) and t is even, then C1 and C2 are self-orthogonal.
+   (d) If p ≡ 5 (mod 12) and t is even, then C1^⊥ = D2 and C2^⊥ = D1. ◆