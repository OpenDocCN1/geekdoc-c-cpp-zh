+   2. The truth value for two terms connected by the = symbol is T if both terms refer to the same entity; otherwise it is F.

+   3. The truth value for ∀x p(x) has value T if p(x) has value T for every assignment to x of an entity in the domain D; otherwise it has value F.

+   4. The truth value for ∃x p(x) has value T if p(x) has value T for at least one assignment to x of an entity in the domain D; otherwise it has value F.

+   5. The operator precedence is as follows: ¬, =, ∧, ∨, ⇒, ⇔ .

+   6. The quantifiers have precedence over the operators.

+   7. Parentheses change the order of the precedence.

**Example 3.11** Suppose our application is considering the four individuals Socrates, Plato, Zeus, and Fido, and we are interested in discussing whether they are human, mortal, and have legs. Our signature can be as follows:

+   1. Constant Symbols = {Socrates, Plato, Zeus, Fido}.

+   2. Predicate Symbols = {human, mortal, legs}. All predicates have arity one.

Let the model have these components:

+   1. D is the set of these four particular individuals.

+   2. The interpretation is as follows:

+   (a) A different individual is assigned to each of the constant symbols.

+   (b) The truth value assignments are given by these tables:

| x | Socrates | Plato | Zeus | Fido |
|---|---|---|---|---|
| human(x) | T | T | F | F |

| x | Socrates | Plato | Zeus | Fido |
|---|---|---|---|---|
| mortal(x) | T | T | F | T |

| x | Socrates | Plato | Zeus | Fido |
|---|---|---|---|---|
| legs(x) | T | T | T | T |

Then we have the following:

+   1. The sentence

```
human(Zeus) ∧ human(Fido) ∨ human(Socrates)
```

has value T because ∧ takes precedence over ∨.