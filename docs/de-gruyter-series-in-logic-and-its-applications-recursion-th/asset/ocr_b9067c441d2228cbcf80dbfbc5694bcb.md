# # 7 Classification of jump operators

The Turing jump operator x ↦ x' is degree invariant, i.e. if x ≡T y then x' ≡T y'. The property of degree invariance is a fundamental property of the operator that motivated the introduction of Martin's conjecture (§ 6.6.5). In this chapter we discuss a stronger one called _uniform degree invariance_ and give a classification of functions that satisfy this property.

# ## 7.1 Uniformly degree invariant functions

**Definition 7.1.1.**
- If e = (e0, e1), we say that x ≡T y via e if x = Φe0^y and y = Φe1^x;
- a function F : 2^ω → 2^ω is _uniformly degree invariant_ on a cone C = {x | x ≥T z} with base z if there is a function t : ω → ω such that for any x, y ≥T z with x ≡T y via e, we have F(x) ≡T F(y) via t(e).

Note that in the definition above, the value of t(e) is independent of the reals x, y.

In 1967, Sacks made a conjecture on the existence of a degree invariant function x ↦ W^x for a general solution of Post's problem. This conjecture contradicts Martin's conjecture since the latter asserts that any such function must be at least as strong as the jump operator:

**Conjecture 7.1.2 (Sacks[119]).** _There is a_ Σ1^1_-predicate_ W ⊆ 2^ω × ω _such that, if_ W^x = {n | W(x, n)}, _then_ x <T W^x < x' _and for any_ y ≡T x, W^x ≡T W^y_._

In 1975, Lachlan [80] proved that this conjecture failed for uniformly degree invariant W.

# ## 7.1.1 Nonincreasing uniformly degree invariant functions

Uniformly degree invariant functions are well-behaved under ZF + DC + AD. The following theorem says that a uniformly degree invariant function is either a constant or increasing on a cone.

**Theorem 7.1.3 (Slaman and Steel [142]).** _Assume_ ZF + DC + AD_. If F is uniformly degree invariant and not increasing on a cone, then F is a constant on a cone._

We decompose the proof of Theorem 7.1.3 into a series of lemmas. Let F be uniformly degree invariant via ↾ a and not increasing on a cone.

**Lemma 7.1.4.** _Assume_ ZF+DC+AD_. If F is uniformly degree invariant and nonincreasing on a cone, then F(x) <T x on a cone._