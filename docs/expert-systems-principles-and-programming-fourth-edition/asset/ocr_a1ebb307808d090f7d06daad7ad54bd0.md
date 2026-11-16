# Table 3.16 Summary of the Purpose of Forward Chaining, Backward Chaining, and Abduction

| Inference | Start | Purpose |
|---|---|---|
| Forward chaining | Facts | Conclusions that must follow |
| Backward chaining | Uncertain conclusion | Facts to support the conclusion |
| Abduction | True conclusion | Facts which may follow |

A number of AI and expert systems have used frame-based abduction for diagnostic problem solving. In these systems, the knowledge base contains causal associations between disorders and symptoms. Inferences are made using generate-and-test of hypotheses for the disorders.

# ## Nonmonotonic Reasoning

Normally the addition of new axioms to a logic system means that more theorems can be proven since there are more axioms from which theorems can be derived. This property of increasing theorems with increasing axioms is known as monotonicity and systems such as deductive logic are called monotonic systems.

However, a problem can occur if a newly introduced axiom partially or completely contradicts a previous axiom. In this case, the theorems that had been proven may no longer be valid. Thus, in a nonmonotonic system, the theorems do not necessarily increase as the number of axioms increases.

The concept of nonmonotonicity has an important application to expert systems. As new facts are generated—which is analogous to theorems being proved—a monotonic expert system would keep building up facts. A major problem can occur if one or more facts becomes false because a monotonic system cannot deal with changes in the truth of axioms and theorems. As a very simple example, suppose there is a fact that asserts the time. As soon as time changes by one second, the old fact is no longer valid. A monotonic system would not be capable of dealing with this situation. As another example, suppose a fact was asserted by an aircraft identification system that a target was hostile. Later, new evidence proves the target is friendly. In a monotonic system, the original identification of hostile could not be changed. A nonmonotonic system allows the retraction of facts.

As another application, suppose you wanted to write an explanation facility for an expert system that would allow a user to go back to previous inferences and explore alternate inference paths of “What if” type questions. All inferences made after the desired previous one must be retracted from the system. Besides facts, rules may also have been excised from the system and so must be put back in the knowledge base for nonmonotonicity. Further complications arise in systems such as OPSS in which rules can be created automatically on the right-hand side of rules during execution. For nonmonotonicity, any inferred rules made after the previous desired inference would have to be excised from the system. Keeping track of all inferences made can consume a lot of memory and significantly slow down the system.