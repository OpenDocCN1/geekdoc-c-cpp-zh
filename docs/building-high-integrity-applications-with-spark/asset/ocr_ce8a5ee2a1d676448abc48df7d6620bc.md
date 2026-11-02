# 5

# Mathematical Background

In this chapter we present some background in mathematical logic in the context of software analysis. This material may be review for some readers, but we encourage all to at least skim this chapter to gain understanding of our notation, terminology, and use in writing SPARK programs. You may wish to consult a discrete mathematics textbook such as those by Epp (2010), Gersting (2014), or Rosen (2011) for a complete treatment of these topics.

# 5.1 Propositional Logic

A proposition is a meaningful declarative sentence that is either true or false. Propositions are also called logical statements or just statements. A statement cannot be true at one point in time and false at another time. Here, for example, are two simple propositions, one true and one false:

+   Sodium Azide is a poison.
+   New York City is the capital of New York state.

Not all statements that can be uttered in a natural language are unambiguously true or false. When a person makes a statement such as, “I like Italian food,” there are usually many subtle qualifications to the meaning at play. The speaker might really mean, “I usually like Italian food,” or, “I’ve had Italian food that I liked.” The true meaning is either evident from the context of the conversation or can be explored in greater depth by asking clarifying questions. In any case, the speaker almost certainly does not mean he or she definitely likes all Italian food in the world. The original statement is neither completely true nor completely false.

Even mathematical expressions may be ambiguous. We cannot tell whether the expression x ≥ 17 is true or false as we do not know the value of x. We can