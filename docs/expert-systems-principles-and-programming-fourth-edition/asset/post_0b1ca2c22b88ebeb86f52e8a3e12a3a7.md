
it's best to limit the number of drugs that a patient receives, even if the patient is thought to be suffering from several different infections. The generator takes the prioritized list from the planner and generates sublists of one or two drugs if possible. These sublists are then tested for efficacy against the infections, patient's allergies, and other considerations before a decision is made to administer them to the patient.

Generate-and-test can also be considered the basic inference paradigm of rules. If the conditional elements of a rule are satisfied, it generates some actions such as new facts. The inference engine tests these facts against the conditional elements of rules in the knowledge base. Those rules that are satisfied are put on the agenda and the top-priority rule generates its actions, which are then tested, and so forth. Thus generate-and-test produces an inference chain that may lead to the correct solution.

## Abduction

Inference by abduction is another method that is commonly used in diagnostic problem solving. The schema of abduction resembles modus ponens, but is actually very different, as shown in Table 3.15.

| Abduction | Modus ponens |
|---|---|
| p → q | p → q |
| q | p |
| ∴ p | ∴ q |

Abduction is another name for a fallacious argument that we discussed in Section 3.6, as the Fallacy of the Converse. Although abduction is not a valid deductive argument, it is a useful method of inference and has been used in expert systems. Like analogy, which also is not a valid deductive argument but is quick and cheap (in reasoning time, not money). Abduction may be useful as a heuristic rule of inference. That is, when we have no deductive method of inference, abduction may prove useful but is not guaranteed to work. Analogy, generate-and-test, and abduction are all methods that are not deductive and are not guaranteed to work all the time. From true premises, these methods cannot prove true conclusions. However, these techniques are useful in reducing the search space by generating reasonable hypotheses, which can then be used with deduction.

Abduction is sometimes referred to as reasoning from observed facts to the best explanation. As an example of abduction, consider the following:

```
IF x is an elephant THEN x is an animal
IF x is an animal THEN x is a mammal
```

If we know that Clyde is a mammal, can we conclude that Clyde is an elephant? The answer to this question depends on whether we are talking about the real world or our expert system. In the real world we could not make this conclusion with any degree of certainty. Clyde could be a dog, cat, cow, or any other kind of animal that was a mammal but not an elephant. In fact, considering how many species of animals there are, the probability of Clyde being an elephant is rather low, without knowing any more information about Clyde.

However, in an expert system with only the preceding rules, we could say by abduction with 100% certainty that if Clyde is a mammal, then Clyde is an elephant. This inference follows from a closed-world-assumption in which we have assumed that nothing else exists outside the closed world of our expert system. Anything that cannot be proven is assumed false in a closed world. Under the closed-world assumption, all the possibilities are known. Since the expert system consists of only these two rules and only an elephant can be a mammal, then if Clyde is a mammal, he must be an elephant.

Suppose we add a third rule, as follows:

```
IF x is a dog THEN x is an animal
```

We can still operate our expert system under the closed-world assumption. However, now we cannot conclude with 100 percent certainty that Clyde is an elephant. All we can be sure of is that Clyde is either an elephant or a dog.

In order to decide between the two, more information is needed. For example, if there is another rule,

```
IF x is a dog THEN x barks
```

and evidence that Clyde barks, the rules can be revised as follows:

- (1) IF x is an animal THEN x is a mammal
- (2) IF x barks THEN x is an animal
- (3) IF x is a dog THEN x barks
- (4) IF x is an elephant THEN x is an animal

Now a backward chain of abductive inference using rules (1), (2), and (3) can be made to show that Clyde must be a dog.

A backward chain of abduction is not the same as the customary meaning of backward chaining. The term backward chaining means that we are trying to prove a hypothesis by looking for evidence to support it. Backward chaining would be used in trying to prove that Clyde is a mammal. Of course, for our small system there are no other possibilities. However, other classifications could be added for reptiles, birds, and so forth.

If it's known that Clyde is a mammal, abduction could be used to determine if Clyde is an elephant or a dog. Forward chaining would be used if it is known that Clyde is an elephant and we wanted to know if he is a mammal. As you can see, the choice of inference method depends on what is to be determined. Since forward chaining is deductive, only its conclusions are always guaranteed valid.

Table 3.16 summarizes the purpose of each of the three inference techniques.

## Table 3.16 Summary of the Purpose of Forward Chaining, Backward Chaining, and Abduction

| Inference | Start | Purpose |
|---|---|---|
| Forward chaining | Facts | Conclusions that must follow |
| Backward chaining | Uncertain conclusion | Facts to support the conclusion |
| Abduction | True conclusion | Facts which may follow |

A number of AI and expert systems have used frame-based abduction for diagnostic problem solving. In these systems, the knowledge base contains causal associations between disorders and symptoms. Inferences are made using generate-and-test of hypotheses for the disorders.

## Nonmonotonic Reasoning

Normally the addition of new axioms to a logic system means that more theorems can be proven since there are more axioms from which theorems can be derived. This property of increasing theorems with increasing axioms is known as monotonicity and systems such as deductive logic are called monotonic systems.

However, a problem can occur if a newly introduced axiom partially or completely contradicts a previous axiom. In this case, the theorems that had been proven may no longer be valid. Thus, in a nonmonotonic system, the theorems do not necessarily increase as the number of axioms increases.

The concept of nonmonotonicity has an important application to expert systems. As new facts are generated—which is analogous to theorems being proved—a monotonic expert system would keep building up facts. A major problem can occur if one or more facts becomes false because a monotonic system cannot deal with changes in the truth of axioms and theorems. As a very simple example, suppose there is a fact that asserts the time. As soon as time changes by one second, the old fact is no longer valid. A monotonic system would not be capable of dealing with this situation. As another example, suppose a fact was asserted by an aircraft identification system that a target was hostile. Later, new evidence proves the target is friendly. In a monotonic system, the original identification of hostile could not be changed. A nonmonotonic system allows the retraction of facts.

As another application, suppose you wanted to write an explanation facility for an expert system that would allow a user to go back to previous inferences and explore alternate inference paths of “What if” type questions. All inferences made after the desired previous one must be retracted from the system. Besides facts, rules may also have been excised from the system and so must be put back in the knowledge base for nonmonotonicity. Further complications arise in systems such as OPSS in which rules can be created automatically on the right-hand side of rules during execution. For nonmonotonicity, any inferred rules made after the previous desired inference would have to be excised from the system. Keeping track of all inferences made can consume a lot of memory and significantly slow down the system.
