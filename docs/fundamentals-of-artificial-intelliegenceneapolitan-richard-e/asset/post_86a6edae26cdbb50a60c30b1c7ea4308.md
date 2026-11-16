
## 3.1.2 Semantics

In first-order logic we first specify a signature, which determines the language. Given a language, a **model** has the following components:

- 1. A nonempty set D of **entities** called a **domain of discourse**.
- 2. An **interpretation**, which consists of the following:
  - (a) An entity in D is assigned to each of the constant symbols. Ordinarily, every entity is assigned to a constant symbol.
  - (b) For each function, an entity is assigned to each possible input of entities to the function.
  - (c) The predicate ‘True’ is always assigned the value T, and the predicate ‘False’ is always assigned the value F.
  - (d) For every other predicate, the value T or F is assigned to each possible input of entities to the predicate.

### Example 3.9

Suppose our application is considering the five individuals mentioned in Example 3.1, and we are only concerned with discussing whether any of them are married and whether any of them are young. Our signature can be as follows:

- 1. Constant Symbols = {Mary, Fred, Sam, Laura, Dave }.
- 2. Predicate Symbols = {married, young}. The predicate ‘married’ has arity two and the predicate ‘young’ has arity one.

One particular model has these components:

- 1. The domain of discourse D is the set of these five particular individuals.
- 2. The interpretation is as follows:
  - (a) A different individual is assigned to each of the constant symbols.
  - (b) The truth value assignments are given by these tables:

| x | Mary | Fred | Sam | Laura | Dave |
|---|---|---|---|---|---|
| young(x) | F | F | T | T | T |

| y \ x | Mary | Fred | Sam | Laura | Dave |
|---|---|---|---|---|---|
| Mary | F | T | F | F | F |
| Fred | T | F | F | F | F |
| Sam | F | F | F | F | F |
| Laura | F | F | F | F | F |
| Dave | F | F | F | F | F |

married(x, y)

### Example 3.10

Suppose our application is considering the three individuals named Dave, Gloria, and Ann, and we are concerned with discussing the mother of each individual and whether each individual loves the other. Our signature can be as follows:

- 1. Constant Symbols = {Dave, Gloria, Ann}.
- 2. Predicate Symbols = {love}. The predicate ‘love’ has arity two.
- 3. Function symbols = {mother}. The function ‘mother’ has arity one.

One particular model has these components:

- 1. The domain of discourse D is the set of these three particular individuals.
- 2. The interpretation is as follows:
  - (a) A different individual is assigned to each of the constant symbols.
  - (b) The truth value assignments are given by this table:

| y \ x | Dave | Gloria | Ann |
|---|---|---|---|
| Dave | F | F | F |
| Gloria | T | F | T |
| Ann | T | T | F |

love(x, y)

  - (c) The function assignments are given by this table:

| x | Dave | Gloria | Ann |
|---|---|---|---|
| mother(x) | Gloria | Ann | - |

Notice that no assignment is made for the mother of Ann. Technically, every entity must be assigned a value by a function. If Ann’s mother is not one of the entities, we can simply use a dummy symbol like the dash (-) as our assignment. In practice, we do not ordinarily reason with first-order logic by completely specifying a model. So we need not concern ourselves with this nuance. Note further that a binary predicate need not be symmetric. Gloria loves Dave but Dave does not love Gloria.

Once a model is specified, the truth values of all sentences are assigned according to the following rules:

- 1. The truth values for sentences developed with the symbols ¬, ∧, ∨, ⇒, and ⇔ are assigned in the same way as done in propositional logic.
- 2. The truth value for two terms connected by the = symbol is T if both terms refer to the same entity; otherwise it is F.
- 3. The truth value for ∀x p(x) has value T if p(x) has value T for every assignment to x of an entity in the domain D; otherwise it has value F.
- 4. The truth value for ∃x p(x) has value T if p(x) has value T for at least one assignment to x of an entity in the domain D; otherwise it has value F.
- 5. The operator precedence is as follows: ¬, =, ∧, ∨, ⇒, ⇔ .
- 6. The quantifiers have precedence over the operators.
- 7. Parentheses change the order of the precedence.

### Example 3.11

Suppose our application is considering the four individuals Socrates, Plato, Zeus, and Fido, and we are interested in discussing whether they are human, mortal, and have legs. Our signature can be as follows:

- 1. Constant Symbols = {Socrates, Plato, Zeus, Fido}.
- 2. Predicate Symbols = {human, mortal, legs}. All predicates have arity one.

Let the model have these components:

- 1. D is the set of these four particular individuals.
- 2. The interpretation is as follows:
  - (a) A different individual is assigned to each of the constant symbols.
  - (b) The truth value assignments are given by these tables:

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

- 1. The sentence

```
human(Zeus) ∧ human(Fido) ∨ human(Socrates)
```

has value T because ∧ takes precedence over ∨.
- 2. The sentence human(Zeus) ∧ (human(Fido) ∨ human(Socrates)) has value F because we changed the order of precedence with the parentheses.
- 3. The sentence ∀x human(x) has value F because human(Zeus) = F and human(Fido) = F.
- 4. The sentence ∀x mortal(x) has value F because mortal(Zeus) = F.
- 5. The sentence ∀x legs(x) has value T because legs(x) = T for every assignment to x.
- 6. The sentence ∃x human(x) has value T because human(Socrates) = T and human(Plato) = T.
- 7. The sentence ∀x (human(x) ⇒ mortal(x)) has value T. The following table shows this:

| x | human(x) | mortal(x) | human(x) ⇒ mortal(x) |
|---|---|---|---|
| Socrates | T | T | T |
| Plato | T | T | T |
| Zeus | F | F | T |
| Fido | F | T | T |

### Example 3.12

Suppose we have the model and interpretation in Example 3.10. Recall that the truth value assignments in that interpretation are given by this table:

| y \ x | Dave | Gloria | Ann |
|---|---|---|---|
| Dave | F | F | F |
| Gloria | T | T | T |
| Ann | T | T | F |

love(x, y)

Then we have the following:

- 1. The sentence

$\exists x \forall y \text{ love}(x, y)$

has value T because love(Gloria,y) has value T for every value of y. This sentence means that there is someone who loves everybody. It is true because Gloria loves everyone.
- 2. The sentence

$\forall x \exists y \text{ love}(x, y)$

has value F because love(Dave,y) does not have value T for any value of y. This sentence means that everyone loves someone. It is false because Dave does not love anyone.

## 3.1.3 Validity and Logical Implication

The notions of a tautology and a fallacy in propositional logic extend to first-order logic. We have the definitions that follow.

### Definition 3.1

If sentence s has value T under interpretation I, we say that I satisfies s, and we write \( I \models s \). A sentence is **satisfiable** if there is some interpretation under which it has value T.

### Example 3.13

The sentence

human(Socrates)

is satisfied in any interpretation that assigns T to human(Socrates).

### Example 3.14

The sentence

$\forall x \text{ human}(x)$

is satisfied in any interpretation that assigns T to human(x) for every individual x in the domain of discourse.

If a formula contains free variables (and therefore is not a sentence), then an interpretation alone does not determine its truth value. We extend the definition of satisfiability to such formulas as follows.

### Definition 3.2

A formula that contains free variables is **satisfied** by an interpretation if the formula has value T regardless of which individuals from the domain of discourse are assigned to its free variables.

### Example 3.15

The formula

love(Socrates, y)

is satisfied by any interpretation that assigns T to love(Socrates, y) for every individual y in the domain of discourse.
