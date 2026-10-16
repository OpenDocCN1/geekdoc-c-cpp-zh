To specify the operational semantics of our sample language, we give reduction rules that specify how the control reduces the constructs of the language to a value. These reduction rules are given in a mathematical notation similar to logical inference rules, so we discuss such logical inference rules first.

# 12.2.1 Logical Inference Rules

Inference rules in logic are written in the following form:

premise
conclusion

That is, the premise, or condition, is written first; then a line is drawn, and the conclusion, or result, is written. This indicates that, whenever the premise is true, the conclusion is also true. As an example, we can express the commutative property of addition as the following inference rule:

a + b = c
b + a = c

In logic, such inference rules are used to express the basic rules of propositional and predicate calculus. As an example of an inference rule in logic, the transitive property of implication is given by the following rule:

a → b, b → c
a → c

This says that if a implies b and b implies c, then a implies c.

Axioms are inference rules with no premise—they are always true. An example of an axiom is a + 0 = a for integer addition. This can be written as an inference rule with an empty premise:

a + 0 = a

More often, this is written without the horizontal line:

a + 0 = a

# 12.2.2 Reduction Rules for Integer Arithmetic Expressions

We use the notation of inference rules to describe the way the control operates to reduce an expression to its value. There are several styles in current use as to how these rules are written. The particular form we use for our reduction rules is called structural operational semantics; an alternative form, called natural semantics, is actually closer to the denotational semantics studied later; see the Notes and References.

We base the semantic rules on the abstract syntax for expressions in our sample language:

E → E₁ ‘+’ E₂ | E₁ ‘−’ E₂ | E₁ ‘*’ E₂ | ‘(’ E₁ ‘)’
N → N₁ D | D
D → ‘0’ | ‘1’ | … | ‘9’

For the time being we can ignore the storage, since this grammar does not include identifiers. We use the following notation: E, E₁, and so on to denote expressions that have not yet been reduced to values; V, V₁, and so on will stand for integer values; E => E₁ states that expression E reduces to expression E₁ by