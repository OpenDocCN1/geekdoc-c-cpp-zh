
In order to provide for nonmonotonicity, it is necessary to attach a justification or dependency to each fact and rule that explains the reason for belief in it. If a nonmonotonic decision is made, then the inference engine can examine the justification of each fact and rule to see if it is still believed, and also to possibly restore excused rules and retracted facts that are believed again.

The problem of justifying facts was first pointed out in the **frame problem**, which is not the same concept as the frames discussed in Chapter 2. The frame problem is a descriptive term named after the problem of identifying what has or has not changed in a movie frame. Motion pictures are photographed as a succession of still pictures, called frames. When played back at 24 frames per second or faster, the human eye cannot distinguish the individual frames and so the illusion of motion results. An AI frame problem is to recognize changes in an environment over time. As an example, consider the Monkey and Bananas problem discussed earlier. Suppose the monkey must step on a red box to reach the bananas and so the action is “push red box under bananas.” Now the frame problem is—how do we know the box is still red after the action? Pushing the box should not change the environment. However, other actions such as “paint the box blue” will change the environment. In some expert-system tools an environment is called a **world** and consists of a set of related facts. An expert system may keep track of multiple worlds to do hypothetical reasoning simultaneously. The problem of maintaining the correctness or truth of a system is called **truth maintenance**. Truth maintenance or a variation called **assumption-based truth maintenance**, is essential for keeping each world pure by retracting unjustified facts.

As a simple example of nonmonotonic reasoning, let’s consider the classic example of Tweety the bird. In the absence of any other information, we would therefore assume that since Tweety is a bird, then Tweety can fly. This is an example of **default reasoning**, much like the defaults used in frame slots. Default reasoning can be considered as a rule that makes inferences about rules, a **metarule** which states:

```
IF X is not known for certain, and
there is no evidence contradicting X
THEN tentatively conclude Y
```

Metarules are discussed more extensively in the next section. In our case the metarule has the more specific form:

```
X is the rule "All birds can fly," and
fact "Tweety is a bird"
Y is the inference "Tweety can fly"
```

In terms of production rules, this can be expressed as a rule in our knowledge base, which says:

```
IF X is a bird THEN X can fly
```

and the fact that exists in working memory:

```
Tweety is a bird
```

Unifying the fact with the antecedent of the rule gives the inference that Tweety can fly.

Now comes the problem. Suppose an additional fact is added to working memory, which says that Tweety is a penguin. We know that penguins cannot fly and so the inference that Tweety can fly is incorrect. Of course, there must be a rule in the system that also states this knowledge or else the fact will be ignored.

In order to maintain the correctness of our system, the incorrect inference must be removed. However, this may not be sufficient if other inferences were based on the incorrect inference. That is, other rules may have used the incorrect inference as evidence to draw additional inferences, and so on. This is a problem of truth maintenance. The inference that Tweety can fly was a plausible inference that is based on default reasoning. The term *plausible* means not impossible and will be discussed further in Chapter 4.

One way of allowing for nonmonotonic inference is by defining a sentential operator M, which can be informally defined as “is consistent.” For example,

```
(∀ x) [Bird(x) ∧ M(Can_fly(x)) -> Can_fly(x)]
```

can be stated as “For every x, if x is a bird and it is consistent that a bird can fly, then x can fly.” The term is *consistent* means that there are no contradictions with other knowledge. However, this interpretation has been criticized as really stating that the only birds that cannot fly are those which have been inferred not capable of flying. This is an example of **autopoietic reasoning**, which literally means reasoning about your own knowledge. Both default and autopoietic reasoning are used in **commonsense reasoning**, which humans generally do quite well but is very difficult for computers.

Autopoietic reasoning is reasoning about your own knowledge as distinct from knowledge in general. Generally, you can do this very well because you know the limits of your knowledge. For example, suppose a total stranger came up and stated you were his spouse. You would immediately know (unless you had amnesia) that you were not their spouse because you had no knowledge of that stranger. The general metarule of autopoietic reasoning is:

```
IF I have no knowledge of X
THEN X is false
```

Notice how autopoietic reasoning relies on the closed-world assumption. Any fact that is not known is assumed false. In autopoietic reasoning, the closed world is your self-knowledge.

Autopoietic and default reasoning are both nonmonotonic. However, the reasons are different. Default reasoning is nonmonotonic because it is **defeasible**. The term defeasible means that any inferences are tentative and may have to be withdrawn as new information becomes available. However, pure autopoietic reasoning is not defeasible because of the closed-world assumption that declares all true knowledge is already known to you. For example, since married people know who is their spouse (unless they want to forget), a married person would not accept that a total stranger was their spouse if they were told that. Because most people recognize that they have imperfect memories, they do not adhere to pure autoepistemic reasoning. Of course, computers do not have this problem until their hard disk crashes.

Autopoietic reasoning is nonmonotonic because the meaning of an autoepistemic statement is context-sensitive. The term context-sensitive means that the meaning changes with the context. As a simple example of context-sensitivity, consider how the word “read” is pronounced in the two sentences:

```
I have read the book
I will read the book
```

The pronunciation of “read” is context sensitive.

Now consider a system consisting of the following two axioms:

```
(∀ x). [Bird(x) ∧ M(Can_fly(x)) → Can_fly (x)]
Bird(Tweety)
```

In this logic system, Can_fly(Tweety) is a theorem derived by unification of Tweety with the variable x and implication.

Now suppose a new axiom is added that states that Tweety cannot fly and thus contradicts the previously derived theorem:

```
~Can_fly(Tweety)
```

The M-operator must change its operation on its argument because now M(Can_fly(Tweety)) is not consistent with the new axiom. In this new context of three axioms, the M-operator would not give a TRUE result for Can_fly(Tweety) because it conflicts with the new axiom. The returned value by the M-operator must be FALSE in this new context, and so the conjunction is FALSE. Thus, there is no implication to produce the theorem Can_fly(Tweety) and no conflict.

One way of implementing this by rules is as follows:

```
IF x is a bird AND x is typical
THEN x can fly
IF x is a bird AND x is nontypical
THEN x cannot fly
```

```
Tweety is a bird
Tweety is nontypical
```

Notice that this system does not invalidate the conclusion Can_fly(Tweety), but rather prevents the incorrect rule from firing at all. This is a much more efficient method of truth maintenance than if we had one rule and the special axiom ~Can_fly(Tweety). Now we have a more general system that can easily handle other nonflying birds such as ostriches without our having to continually add new inferences, which is what the system is supposed to do.

## 3.16 METAKNOWLEDGE

The Classic Meta-DENDRAL program used induction to infer new rules of chemical structure. Meta-DENDRAL was an attempt to overcome the knowledge bottleneck of trying to extract molecular structural rules from human experts. Some expert system tools come with programs to induce rules.

For example, the following classic metarule is taken from the TEIRESIAS knowledge acquisition program for MYCIN, the expert system to diagnose blood infections and meningitis:

```
METARULE 2
IF
The patient is a compromised host, and
There are rules which mention in their premise
pseudomonas, and
There are rules which mention in their premise
klebsiellas
THEN
There is suggestive evidence (0.4) that the former
should be done before the latter
```

The number 0.4 in the action of the rule is a degree of certainty and will be discussed in a later chapter.

TEIRESIAS acquires knowledge interactively from an expert. If a wrong diagnosis has been made by MYCIN, then TEIRESIAS will lead the expert back through the chain of incorrect reasoning until the expert states where the incorrect reasoning started. While going back through the reasoning chain, TEIRESIAS will also interact with the expert to modify incorrect rules or acquire new rules.

Knowledge about new rules is not immediately put into MYCIN. Instead, TEIRESIAS checks to see if the new rule is compatible with similar rules. For example, if the new rule describes how an infection enters the body and other accepted rules have a conditional element stating the portal of entry to the body, then the new rule should also. If the new rule does not state the portal of entry, then TEIRESIAS will query the user about this discrepancy. TEIRESIAS has a rule model pattern of similar rules that it knows about, and tries to fit the new rule into its rule model. In other words, the rule model is the knowledge that TEIRESIAS has about its knowledge. An analogous situation for a human would occur if you went to a car dealer to buy a new car and the dealer tried to sell you a car with three wheels.

The metaknowledge of TEIRESIAS is of two types. The METARULE 2, described previously, is a control strategy that tells how rules are to be applied. In contrast, the rule model type of metaknowledge determines if the new rule is in the appropriate form to be entered in the knowledge base. In a rule-based expert system, determining if the new rule is in the correct form is called verification of the rule. Determining that a chain of correct inferences leads to the correct answer is called validation. Validation and verification are so interdependent
