+   (a) An atomic formula
+   (b) The operator \(\neg\) followed by a formula
+   (c) Two formulas separated by \(\lor, \land, \Rightarrow, \text{or } \Leftrightarrow\)
+   (d) A quantifier following by a variable followed by a formula

4. A sentence is a formula with no free variables.

Rule 4 bears clarification. Consider the following formulas:

```
\(\forall x \text{ love}(x, y) \qquad \forall x \text{ tall}(x).\) (3.1)
```

We discuss shortly what formulas like this mean. Currently, we present them to clarify the definition of a sentence. A variable in a formula is **free** if it is not quantified by the \(\forall\) or the \(\exists\) symbol; otherwise it is **bound**. The formula on the left in Expression 3.1 contains the free variable \(y\) and therefore is not a sentence, whereas the formula on the right does not contain any free variables and therefore is a sentence.

Mathematically, this is all there is to say about the formal language of first-order logic. However, like propositional logic, first-order logic was developed to make statements about the real world and to reason with these statements. The next examples illustrate such statements.

**Example 3.1** As discussed more formally in the next section, in first-order logic we have a **domain of discourse**. This domain is a set and each element in the set is called an **entity**. Each constant symbol identifies one entity in the domain. For example, if we are considering all individuals living in a certain home, our constant symbols could be their names. If there are five such individuals, the constant symbols might be ‘Mary’, ‘Fred’, ‘Sam’, ‘Laura’, and ‘Dave’.

**Example 3.2** A predicate denotes a relationship among a set of entities or a property of a single entity. For example,
married(Mary,Fred)
denotes that Mary and Fred are married, and
young(Sam)
denotes that Sam is young. The number of arguments in a predicate is called its **arity**. The predicate ‘married’ has arity two while the predicate ‘young’ has arity one.

**Example 3.3** If our application is considering the five individuals mentioned in Example 3.1, and we are only concerned with discussing whether any of them are married and whether any of them are young, then our signature would consist of the constant symbols ‘Mary’, ‘Fred’, ‘Sam’, ‘Laura’, and ‘Dave’ and the predicates ‘married’ and ‘young’, where ‘married’ has arity two and ‘young’ has arity one.