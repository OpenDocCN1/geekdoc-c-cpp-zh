# 26.6.3.4 Random number engine requirements

A *random number engine* (commonly shortened to *engine*) e of type E is a uniform random bit generator that additionally meets the requirements (e.g., for seeding and for input/output) specified in this subclause.

At any given time, e has a state eᵢ for some integer i ≥ 0. Upon construction, e has an initial state e₀. An engine’s state may be established via a constructor, a seed function, assignment, or a suitable operator>>.

E’s specification shall define:

+   1. (3.1) — the size of E’s state in multiples of the size of `result_type`, given as an integral constant expression;
+   2. (3.2) — the *transition algorithm* TA by which e’s state eᵢ is advanced to its *successor state* eᵢ₊₁; and
+   3. (3.3) — the *generation algorithm* GA by which an engine’s state is mapped to a value of type `result_type`.

A class E that meets the requirements of a uniform random bit generator (26.6.3.3) also meets the requirements of a *random number engine* if the expressions shown in Table 94 are valid and have the indicated semantics, and if E also meets all other requirements of this subclause 26.6.3.4. In that Table and throughout this subclause:

+   1. (4.1) — T is the type named by E’s associated `result_type`;
+   2. (4.2) — e is a value of E, v is an lvalue of E, x and y are (possibly const) values of E;
+   3. (4.3) — s is a value of T;
+   4. (4.4) — q is an lvalue meeting the requirements of a seed sequence (26.6.3.2);
+   5. (4.5) — z is a value of type `unsigned long long`;
+   6. (4.6) — os is an lvalue of the type of some class template specialization `basic_ostream<charT, traits>`; and
+   7. (4.7) — is is an lvalue of the type of some class template specialization `basic_istream<charT, traits>`;

where `charT` and `traits` are constrained according to Clause 21 and Clause 29.

Table 94: Random number engine requirements

| Expression | Return type | Pre/post-condition | Complexity |
|---|---|---|---|
| `E()` |  | Creates an engine with the same initial state as all other default-constructed engines of type E. | O(size of state) |
| `E(x)` |  | Creates an engine that compares equal to x. | O(size of state) |
| `E(s)` |  | Creates an engine with initial state determined by s. | O(size of state) |
| `E(q)` |  | Creates an engine with an initial state that depends on a sequence produced by one call to q.generate. | same as complexity of q.generate called on a sequence whose length is size of state |
| `e.seed()` | `void` | *Postconditions:* e == E(). | same as E() |
| `e.seed(s)` | `void` | *Postconditions:* e == E(s). | same as E(s) |
| `e.seed(q)` | `void` | *Postconditions:* e == E(q). | same as E(q) |
| `e()` | `T` | Advances e’s state eᵢ to eᵢ₊₁ = TA(eᵢ) and returns GA(eᵢ). | per 26.6.3.3 |
| `e.discard(z)` | `void` | Advances e’s state eᵢ to eᵢ₊z by any means equivalent to z consecutive calls e(). | no worse than the complexity of z consecutive calls e() |