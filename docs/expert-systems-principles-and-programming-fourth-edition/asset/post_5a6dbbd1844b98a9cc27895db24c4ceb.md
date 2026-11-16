
## Figure 3.14 Types of Inference

![](img/2c460d4de56b7ffaad3834eee20beaa0_147_0.png)

used for applications ranging from better speech understanding to more efficient construction of ontologies. The interesting thing is that the adage, “Bigger is better,” does not always hold. In the following communication from Doug Lenat (personal email) he explains why:

> “3 million rules have been entered by hand; through generalization and factoring we have that number down to 1.5 million today. We try to make the number as small as possible, not as large—we could easily expand this into over a billion rules, e.g. Consider 2 types of animals—no rat is also a camel. Knowing 10,000 animals, one could write 100,000,000 rules of that sort. Instead, Cyc has 10,001 rules: Linnaean taxon relationships plus a rule that says that two taxa that aren’t known to stand in a gen/spec relationship are disjoint. The “tens of thousands of rules” is talking about a very special type of rule, namely one of a certain level of complexity, through which NONE of the assertions I just mentioned would count as rules at all.”

We have a couple million assertions because that's as few as we can give away with for the content. We don’t TRY to make the number large, because it would slow things down, but if we WANTED it to be large we could take 10,001 of the (2 million) assertions in the current knowledge base, and equivalently replace them with 100,000,000 only slightly less general-seeming rules. That would be bad.

The application of fuzzy logic to commonsense reasoning is discussed in Chapter 5.

One of the most often-used methods of drawing inferences is deductive logic, which has been used since ancient times to determine the validity of an argument. Although people commonly use the word argument to describe an angry “exchange of views,” it has a very different meaning in logic. A logical argument is a group of statements in which the last is claimed to be justified on the basis of the previous ones in the chain of reasoning. One type of logical argument is syllogism, which was discussed in Chapter 2. As an example of a syllogism:

```
Premise: Anyone who can program is intelligent
Premise: John can program
Conclusion: Therefore, John is intelligent
```

In an argument the premises are used as evidence to support the conclusions. The premises are also called the antecedent and the conclusion is called the consequent. The essential characteristic of deductive logic is that the true conclusion must follow from true premises. A line is customarily drawn to separate the premises from the conclusion, as shown above, so that it is not necessary to explicitly label the premises and conclusion.

The argument could have been written more briefly as:

```
Anyone who can program is intelligent
John can program
.. John is intelligent
```

where the three dots, .., mean “therefore.”

Let’s take a closer look at syllogistic logic now. The main advantage of studying syllogisms is that it is a simple, well-understood branch of logic that can be completely proven. Also, syllogisms are often useful since they can be expressed in terms of IF-THEN rules. For example, the previous syllogism can be rephrased as:

```
IF Anyone who can program is intelligent and
John can program
THEN John is intelligent
```

In general, a syllogism is any valid deductive argument having two premises and a conclusion. The classic syllogism is a special type called a categorical syllogism. The premises and conclusions are defined as categorical statements of the following four forms, as shown in Table 3.2.

| Form | Schema | Meaning |
| :--- | :--- | :--- |
| A | All S is P | universal affirmative |
| E | No S is P | universal negative |
| I | Some S is P | particular affirmative |
| O | Some S is not P | particular negative |

Note that in logic, the term *schema* specifies the logical form of the statement. This also illustrates another use of the word schema, which is different from its AI use, discussed in Chapter 2. In logic, the word schema is used to show the essential form of an argument. Schemata may also specify the logical form of an entire syllogism as in:

```
All M is P
All S is M
.: All S is P
```

The subject of the conclusion, S, is called the **minor term** while the predicate of the conclusion, P, is called the **major term**. The premise containing the major term is called the **major premise** and the premise containing the minor term is called the **minor premise**. For example:

```
Major Premise: All M is P
Minor Premise: All S is M
Conclusion: All S is P
```

is a syllogism said to be in **standard form**, with its major and minor premises identified. The **subject** is the object that is being described while the **predicate** describes some property of the subject. For example, in the statement:

```
All microcomputers are computers
```

the subject is “microcomputers” and the predicate is “computers.” In the statement:

```
All computers with 1 Gigabyte of RAM
are computers with a lot of memory
```

the subject is “computers with 1 Gigabyte” and the predicate is “computers with a lot of memory.”

The forms of the categorical statements have been identified since ancient times by the letters A, E, I, and O. The A and I indicate affirmative and are thought to come from the first two vowels of the Latin word *affirmo* (I affirm); while E and O come from *neggo* (I negate). The A and I forms are said to be **affirmative in quality** by affirming that the subjects are included in the predicate class. The E and O forms are **negative in quality** because the subjects are excluded from the predicate class.

The verb is comes from **copula** in Latin, which means to connect. The copula connects the two parts of the statement. In the standard categorical syllogism, the copula is the present tense form of the verb *to be*. So another version is:

```
All S are P
```

The third term of the syllogism, M, is called the **middle term** and is common to both premises. The middle term is essential because a syllogism is defined such that the conclusion cannot be inferred from either of the premises alone. So the argument:

```
All A is B
All B is C
.: All A is B
```

is not a valid syllogism since it follows from the first premise alone.

The **quantity** or **quantifier** describes the portion of the class included. The quantifiers **All** and **No** are **universal** because they refer to entire classes. The quantifier **Some** is called **particular** because it refers to just part of the class.

The **mood** of a syllogism is defined by the three letters that give the form of the major premise, minor premise, and conclusion, respectively. For example, the syllogism:

```
All M is P
All S is M
.: All S is P
```

is an AAA mood.

There are four possible patterns of arranging the S, P, and M terms, as shown in Table 3.3. Each pattern is called a figure, with the number of the **figure** specifying its type.

| | Figure 1 | Figure 2 | Figure 3 | Figure 4 |
|---|---|---|---|---|
| Major Premise | MP | PM | MP | PM |
| Minor Premise | SM | SM | MS | MS |

So the previous example is completely described as an AAA-1 syllogism type. Just because an argument has a syllogistic form does not mean that it is a valid syllogism. Consider the AAA-1 syllogism form:

```
All M is P
No S is M
.: No S is P
```

which is not a valid syllogism, as can be seen from the example:

```
All microcomputers are computers
No mainframe is a microcomputer
.: No mainframe is a computer
```

Rather than trying to think up examples to prove the validity of syllogistic arguments, there is a **decision procedure** that can be used. A decision procedure is a method of proving validity. A decision procedure is some general mechanical method or algorithm by which the process of determining validity can be automated. While there are decision procedures for syllogistic logic and propositional logic, Church showed in 1936 that there is none for predicate logic. Instead, people or computers must apply creativity to generate proofs. In the 1970s, programs such as the Automated Mathematician and Eurisko by Doug Lenat rediscovered mathematical proofs of the Goldbach’s Conjecture and the Unique Factorization Theorem. Mathematical journals have not been keen on publishing creative works by computers in the same way literary journals and magazines have not exactly encouraged the submission of poems or novels by computers. (They’re only willing to pay a little bit.)

The decision procedure for propositions is simply constructing a truth table and examining it for tautology. The decision procedure for syllogisms can be done using Venn diagrams with three overlapping circles representing S, P, and M, as shown in Figure 3.15a. For the syllogism form AEE-1:

```
All M is P
No S is M
.. No S is P
```

the major premise is illustrated in Figure 3.15b. The lined section of M indicates that there are no elements in that portion. In Figure 3.15c the minor premise is included by lining its portion with no elements. From Figure 3.15c it can be seen that the conclusion of EAE-1 is false since there are some S in P. As another example, the following EAE-1 is valid as can be seen from Figure 3.16c:

```
No M is P
All S is M
.. No S is P
```

Venn diagrams that involve “some” quantifiers are a little more difficult to draw. The general rules for drawing categorical syllogisms under the Boolean view that there may be no members in the A and E statements are:

![](img/2c460d4de56b7ffaad3834eee20beaa0_151_0.png)
