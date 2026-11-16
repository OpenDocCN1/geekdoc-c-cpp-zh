![](bbox=[0.08, 0.08, 0.46, 0.18])

![](bbox=[0.55, 0.08, 0.95, 0.15])

![](bbox=[0.1, 0.2, 0.9, 0.3])

8. Design circuits to implement the input/output tables for addition, as given in Figure 1.8. Try to make your circuits as simple as possible. (The circuits that are used in real computers for this purpose are more simplified than the ones you will probably come up with, but the general approach of using logic to design computer circuits is valid.)

# 1.4 Predicates and Quantifiers

In propositional logic, we can let p stand for “Roses are red” and q stand for “Violets are blue.” Then p ∧ q will stand for “Roses are red and violets are blue.” But we lose a lot in the translation into logic. Since propositional logic only deals with truth values, there’s nothing we can do with p and q in propositional logic that has anything to do with roses, violets, or color. To apply logic to such things, we need predicates.

The type of logic that uses predicates is called predicate logic, or, when the emphasis is on manipulating and reasoning with predicates, predicate calculus.

A predicate is a kind of incomplete proposition, which becomes a proposition when it is applied to some entity (or, as we’ll see later, to several entities). In the proposition “the rose is red,” the predicate is red. By itself, “is red” is not a proposition. Think of it as having an empty slot, that needs to be filled in to make a proposition: “— is red.” In the proposition “the rose is red,” the slot is filled by the entity “the rose,” but it could just as well be filled by other entities: “the barn is red”; “the wine is red”; “the banana is red.” Each of these propositions uses the same predicate, but they are different propositions and they can have different truth values.

If P is a predicate and a is an entity, then P(a) stands for the proposition that is formed when P is applied to a. If P represents “is red” and a stands for “the rose,” then P(a) is “the rose is red.” If M is the predicate “is mortal” and s is “Socrates,” then M(s) is the proposition “Socrates is