
A on the exam; she also realizes that a smart person is more likely to get an A on the exam. She learns that Joe got an A. When Joe tells her that he did not study very hard, she reasons that Joe is probably smart. By 1990, the modeling of such probabilistic inference became commonplace in AI; such inference is the focus of Part II.

Intelligent behavior is not limited to human reasoning. Evolution itself seems pretty smart in that creatures better able to adapt to their environment tend to survive, with the result being the existence of humans themselves. Researchers in evolutionary computation have solved interesting problems based on a model of natural selection. The actions of non-intelligent entities acting in groups sometimes results in a type of emergent intelligence, called swarm intelligence, and useful algorithms have been developed based on this model. We call both these types of intelligence **emergent intelligence**. Algorithms based on emergent intelligence are discussed in Part III.

In Parts I and II we assume the system is created from knowledge extracted from humans, who are often experts in some domain. However, an important aspect of intelligence involves acquiring new knowledge from experience or data. Part IV concerns learning both logical and probabilistic models from data. Finally, Part V discusses an important endeavor in AI, namely natural language understanding.

## Part I

### Logical Intelligence

## Chapter 2

### Propositional Logic

![](img/67fa924962ee21b3590be9f3b10d9fe7_26_0.png)

Propositional logic concerns propositions/statements, which we assume to be true or false, and the deductive inference of the truth of other propositions from the ones whose truth states we assume to know. By **deductive inference** we mean a process by which the truth of the conclusion is demonstrated to necessarily follow from the truth of the premises. This variation of a classic example illustrates such a deduction:

- Socrates is a man.
- If Socrates is a man, then Socrates is mortal.
- Therefore, Socrates is mortal.

If we assume we know that Socrates is a man and we believe that “If Socrates is a man, then Socrates is mortal” is a true statement, then most of us would reason that Socrates is mortal. Propositional logic does not ask whether this line of reasoning makes sense. Rather, it mathematically models this and other common types of deductive inference that most of us agree make sense. When we incorporate such inference in an artificial intelligence algorithm, we call the algorithm **logic-based**.

In Section 2.1 we provide the basic properties of propositional logic. Section 2.2 develops an inference method called resolution theorem proving, which is the strategy used in many automatic reasoning programs. Section 2.3 shows artificial intelligence applications of propositional logic.

### 2.1 Basics of Propositional Logic

Propositional logic is discussed starting with its syntax and its semantics.

### 2.1.1 Syntax

A **formal language** is a set of words or expressions that are obtained using an alphabet and rules. The **alphabet** for a formal language is the set of **symbols** from which each word is constructed. The set of **rules**, called the **syntax** of the language, specifies how elements of the alphabet are combined to construct words. These words are called **well-formed strings** of symbols.

**Propositional logic** consists of a formal language and semantics that give meaning to the well-formed strings, which are called **propositions**.
The alphabet of propositional logic contains the following symbols:

1. The letters of the English alphabet; that is, A, B, C, ..., Z, and each of these letters with an index (e.g., A4).
2. The logical values True and False.
3. These special symbols:
   - ¬ (NOT)
   - ∧ (AND)
   - ∨ (OR)
   - ⇒ (IF-THEN)
   - ⇔ (IF AND ONLY IF)
   - ( ) (GROUPING).

The symbol ¬ is called a **unary connective** and the symbols ∧, ∨, ⇒, and ⇔ are called **binary connectives**.

The rules for creating propositions are as follows:

1. All letters, all indexed letters, and the logical values True and False are propositions. They are called **atomic propositions**.
2. If _A_ and _B_ are propositions, then so are ¬_A_, _A_ ∧ _B_, _A_ ∨ _B_, _A_ ⇒ _B_, _A_ ⇔ _B_, and (_A_). They are called **compound propositions**.

The compound proposition $\neg A$ is called the **negation** of $A$, $A \wedge B$ is called the **conjunction** of $A$ and $B$, and $A \vee B$ is called the **disjunction** of $A$ and $B$.

Notice that we used italicized letters to refer to propositions. Such letters denote variables whose values can be propositions that are either atomic or compound. In this way we can recursively define compound propositions. These italicized letters are not part of the alphabet.

**Example 2.1** Suppose P and Q are atomic propositions. Then applying Rule 2 once using the $\wedge$ connective, we have that P$\wedge$Q is a proposition. Applying Rule 2 to this compound proposition and the atomic proposition R using the $\vee$ connective, we have that P$\wedge$Q$\vee$R is a proposition.

Mathematically, this is all there is to say about the formal language of propositional logic. However, propositional logic was developed to make statements about the real world and to reason with these statements. The next example illustrates such statements.

**Example 2.2** Suppose the propositions P and Q stand for these statements about the world:

- P: It is raining outside.
- Q: The pavement is wet.

Then the following compound propositions stand for these statements about the world:

- $\neg$P: It is not raining outside.
- P$\wedge$Q: It is raining outside and the pavement is wet.
- P$\vee$Q: It is raining outside or the pavement is wet.
- P$\Rightarrow$Q: If it is raining outside, then the pavement is wet.
- P$\Leftrightarrow$Q: It is raining outside if and only if the pavement is wet.

**Example 2.3** Let P, Q, and R stand for these statements about the world:

- P: It is raining outside.
- Q: The pavement is wet.
- R: The sprinkler is on.

Then applying Rule 2 once using the $\vee$ connective, we have that P$\vee$R is a proposition. Applying Rule 2 a second time using the $\wedge$ connective, we obtain that Q$\wedge$P$\vee$R is a proposition. This proposition stands for the following statement about the world:

- Q$\wedge$P$\vee$R: The pavement is wet and it is raining outside or the sprinkler is on.

### 2.1.2 Semantics

When you saw Example 2.3, you may have asked which of the following is meant by the proposition Q∧P∨R:

1. It is both true that the pavement is wet *and* true that it is raining outside or the sprinkler is on.
2. It is *either* true that the pavement is wet and it is raining outside *or* true that the sprinkler is on.

Next we present the semantics of propositional logic, which answers this question.

The syntax of propositional logic is only concerned with developing propositions; it has nothing to do with attaching meaning to them. As mentioned previously, we need not even associate statements about the world with the propositions. The semantics of propositional logic gives meaning to the propositions. The semantics consists of rules for assigning either the value T (true) or F (false) to every proposition. Such an assignment is called the **truth value** of the proposition. If a proposition has truth value T, we say it is true; otherwise, we say it is false.

The **semantics** for propositional logic consist of the following rules:

1. The logical value True is always assigned the value T and the logical value False is always assigned the value F.
2. Every other atomic proposition is assigned a value T or F. The set of all these assignments constitutes a **model** or **possible world**. All possible worlds (assignments) are permissible.
3. The truth values obtained by applying each connective to arbitrary propositions are given by the following **truth tables**:

| A | ~A |
|---|---|
| T | F |
| F | T |

| A | B | A ^ B |
|---|---|---|
| T | T | T |
| T | F | F |
| F | T | F |
| F | F | F |

| A | B | A v B |
|---|---|---|
| T | T | T |
| T | F | T |
| F | T | T |
| F | F | F |

| A | B | A => B |
|---|---|---|
| T | T | T |
| T | F | F |
| F | T | T |
| F | F | T |

| A | B | A <=> B |
|---|---|---|
| T | T | T |
| T | F | F |
| F | T | F |
| F | F | T |

4. The truth value for compound propositions such as P∧Q∨R are determined recursively using the above truth tables. This is done according to the following rules:
