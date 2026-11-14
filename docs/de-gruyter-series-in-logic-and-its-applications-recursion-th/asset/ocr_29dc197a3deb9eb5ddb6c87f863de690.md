# 3 Admissibility and constructibility

This chapter introduces the basic notions of effective computability from the set-theoretic perspective. While somewhat abstract at first sight, they are natural when viewed from the standpoint of definability.

An admissible structure is essentially an inner model of computation. The constructive universe \( L \) is defined via a transfinite iteration of the Gödel operators. By considering an appropriate initial segment of \( L \) which forms an admissible structure, we will see how a \( \Pi^1_1 \)-set assumes the role of an r.e. set in higher recursion theory.

# 3.1 Kripke–Platek set theory

The Kripke–Platek (KP) theory of sets was developed by Kripke [75] and Platek [113]. KP is a weak version of the ZF axiom system and captures the basic features of effective computation in the setting of set theory. It offers a natural platform for the study in domains beyond \( \omega \).

# 3.1.1 KP

Definition 3.11.1. Let \( \mathscr{L} \) denote the language of ZF. The collection of \( \Delta_0 \)-formulas in \( \mathscr{L} \) is the smallest collection \( X \) consisting of the atomic formulas of \( \mathscr{L} \) and closed under the following operations:
(i) If \( \varphi \in X \) then \( \neg \varphi \in X \).
(ii) If \( \varphi, \psi \in X \), then \( \{ \varphi \land \psi, \varphi \lor \psi \} \subseteq X \).
(iii) If \( \varphi \in X \), then \( \{ (\forall u \in v)\varphi, (\exists u \in v)\varphi \} \subseteq X \).

In (iii) above, both of the formulas \( (\forall u \in v)\varphi \) or \( (\exists u \in v)\varphi \) are called *bounded formulas*. A prefix of the form \( \exists u \in v \) or \( \forall u \in v \) is a *bounded quantifier*. \( \Delta_0 \)-formulas are analogs of *primitive recursive predicates* in recursion theory.

Definition 3.12.1. A \( \Delta_0 \)-formula is also known as a \( \Sigma_0 \)-formula as well as a \( \Pi_0 \)-formula. In general, a formula \( \varphi(u) \) is \( \Sigma_{n+1} \) if it is of the form \( (\exists v)\psi(u, v) \) where \( \psi \) is a \( \Pi_n \)-formula. A formula \( \varphi(u) \) is \( \Pi_{n+1} \) if it is of the form \( (\forall v)\psi(u, v) \) where \( \psi \) is a \( \Sigma_n \)-formula.

Definition 3.13.3. The class of \( \Sigma \)-formulas is the smallest class \( X \) consisting of the \( \Delta_0 \)-formulas and closed under conjunction, disjunction, bounded quantification, and if \( \varphi \in X \) then \( (\exists u)\varphi \in X \).

The class of \( \Pi \)-formulas is the smallest class \( X' \) consisting of the \( \Delta_0 \)-formulas, closed under conjunction, disjunction, bounded quantification, and if \( \varphi \in X' \) then \( (\forall u)\varphi \in X' \).