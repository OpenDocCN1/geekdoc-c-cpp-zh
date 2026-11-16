# 2.1.2 Semantics

When you saw Example 2.3, you may have asked which of the following is meant by the proposition Q∧P∨R:

+   1. It is both true that the pavement is wet *and* true that it is raining outside or the sprinkler is on.

+   2. It is *either* true that the pavement is wet and it is raining outside *or* true that the sprinkler is on.

Next we present the semantics of propositional logic, which answers this question.

The syntax of propositional logic is only concerned with developing propositions; it has nothing to do with attaching meaning to them. As mentioned previously, we need not even associate statements about the world with the propositions. The semantics of propositional logic gives meaning to the propositions. The semantics consists of rules for assigning either the value T (true) or F (false) to every proposition. Such an assignment is called the **truth value** of the proposition. If a proposition has truth value T, we say it is true; otherwise, we say it is false.

The **semantics** for propositional logic consist of the following rules:

+   1. The logical value True is always assigned the value T and the logical value False is always assigned the value F.

+   2. Every other atomic propositions is assigned a value T or F. The set of all these assignments constitutes a **model** or **possible world**. All possible worlds (assignments) are permissible.

+   3. The truth values obtained by applying each connective to arbitrary propositions are given by the following **truth tables**:

| A | ~A |
|---|---|
| T | F |
| F | T |

| A | B | A ^ B |
|---|---|---|
| T | T | T |
| T | F | F |
| F | T | F |
| F | F | F |

| A | B | A v B |
|---|---|---|
| T | T | T |
| T | F | T |
| F | T | T |
| F | F | F |

| A | B | A => B |
|---|---|---|
| T | T | T |
| T | F | F |
| F | T | T |
| F | F | T |

| A | B | A <=> B |
|---|---|---|
| T | T | T |
| T | F | F |
| F | T | F |
| F | F | T |

+   4. The truth value for compound propositions such as P∧Q∨R are determined recursively using the above truth tables. This is done according to the following rules: