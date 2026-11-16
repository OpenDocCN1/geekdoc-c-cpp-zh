
## Logic Programming

inheritance. The full object-oriented language embedded within CLIPS is called COOL (Common Object-Oriented Language). The operation of COOL is transparent to the user so you just have to understand the features of object-oriented programming.

One of the first AI applications of computers was in proving logic theorems with the Logic Theorist program of Newell and Simon. This program was first reported at the Dartmouth Conference on AI in 1956 and caused a sensation because electronic computers previously had been used only for numeric calculations. Now a computer was mechanically reasoning the proofs of mathematical theorems, which had been a task that only mathematicians were thought capable of doing. The term mechanical means automated and dates back to Babbage's Mechanical computer of the nineteenth century.

In the Logic Theorist and its successor, the General Problem Solver (GPS), Newell and Simon concentrated on trying to implement powerful algorithms that could solve any problem. While the Logic Theorist was meant only for mathematical theorem proving, GPS was designed to solve any kind of logic problem, including games and puzzles such as chess, Tower of Hanoi, Missionaries and Cannibals, and cryptarithmetic. An example of their famous cryptarithmetic (secret arithmetic) puzzle is:

```
DONALD
+ GERALD
ROBERT
```

and it is known that D=5. The object is to figure out the arithmetic values of the other letters in the range 0-9.

GPS was the first problem solving program to clearly separate the problem-solving knowledge from the domain knowledge. This paradigm of explicitly separating the problem-solving knowledge from the domain knowledge is now used as the basis of expert systems. In expert systems today, the inference engine decides what knowledge should be used and how it should be applied.

Efforts continued to improve mechanical theorem proving. By the early 1970s, it had been discovered that computation is a special case of mechanical, logical deduction. When backward chaining was applied to sentences of the form "conclusion if conditions", it was powerful enough for significant theorem proving. The conditions can be thought of as representing patterns to be matched as in production rules discussed earlier. Sentences expressed in this form are called Horn clauses after Alfred Horn, who first investigated them. In 1972, the language PROLOG was created by Kowalski, Colmerauer, and Roussel to implement logic programming by backward chaining using Horn clauses.

Backward chaining can be used both to express the knowledge in a declarative representation and also control the reasoning process. Typically, backward chaining proceeds by defining smaller subgoals that must be satisfied if the initial goal is to be satisfied. These subgoals are then further broken down into smaller subgoals and so forth.

An example of declarative knowledge is the following classic example:

```
All men are mortal
Socrates is a man
```

which can be expressed in the Horn clauses:

```
someone is mortal
if someone is a man
Socrates is a man
if (in all cases)
```

For the sentence about Socrates, the IF condition is true in all cases. In other words, the knowledge about Socrates does not require any pattern to match. Contrast this with the mortal case in which someone must be a man for the pattern of the IF condition to be satisfied.

Notice that a Horn clause can be interpreted as a procedure that tells how to satisfy a goal. That is, to determine if someone is mortal, it is necessary to determine if someone is a man. As a slightly more complex example:

```
A car needs gas, oil, and inflated tires to run
```

which can be expressed in a Horn clause as:

```
x is a car and runs
if x has gas and
if x has oil and
if x has inflated tires
```

Notice how the problem of determining if a car will run has been reduced to three simpler subproblems or subgoals. Now suppose there is some additional declarative knowledge as follows:

```
The fuel gauge shows not-empty if a car has gas
The dipstick shows not-empty if a car has oil
The air pressure gauge shows at least 20 if a car
has inflated tires
The fuel gauge shows not-empty
The dipstick reads empty
The air pressure gauge shows 15
```

These can be translated into the following Horn clauses:

```
x has gas
if the fuel gauge shows not-empty
x has oil
if the dipstick shows not-empty
x has inflated tires
if the air pressure gauge shows at least 20
```

```
Fuel gauge is not empty
if (in all cases)
Dipstick reads empty
Air pressure is 15
if (in all cases)
```

From these clauses, a mechanical theorem prover can prove that the car will not run because there is no oil and insufficient air pressure.

One of the advantages of backward-chaining systems is that execution can proceed in parallel. That is, if multiple processors were available, they could work on satisfying subgoals simultaneously. PROLOG is more than just a language since it incorporates a backward-chaining inference engine. At a minimum, PROLOG is a shell since it requires:

- an interpreter or inference engine
- a database (facts and rules)
- a form of pattern matching called unification
- a backtracking mechanism to pursue alternate subgoals if a search to satisfy a goal is unsuccessful.

As an example of backward chaining, suppose you can pay for the oil to make the car run if you have cash or a credit card. One subgoal is checked to see if you have cash. If there is no fact that you do have cash, the backtracking mechanism will then explore the other subgoal to see if you have a credit card. If you have a credit card, the goal of paying for oil can be satisfied. Notice that the absence of a fact to prove a goal is just as effective, although perhaps less efficient, than a negative fact such as “Dipstick reads empty.” Either negative facts or missing facts can cause a goal to be unsatisfied (except in political logic).

If the backtracking and pattern-matching mechanisms are not needed by the problem, then the programmer must work around them or code in a different language. One of the advantages of logic programming is executable specifications. That is, specifying the requirements of a problem by Horn clauses produces an executable program. This is very different from conventional programming in which the requirements document does not look at all like the final executable code.

Unlike production rule systems, the order in which subgoals, facts, and rules are entered in a PROLOG program has significant effects. Efficiency, and therefore speed, are affected by the way that PROLOG searches its database. Furthermore, there are programs that execute correctly if subgoals, facts, and rules are entered one way but go into an infinite loop or have a run-time error if the order changes.

## Expert Systems

Expert systems can be considered declarative programming because the programmer does not specify how a program is to achieve its goal at the level of an algorithm. For example, in a rule-based expert system, any of the rules may become activated and put on the agenda if its LHS matches the facts. The order that the rules were entered does not affect which rules are activated. Thus, the program statement order does not specify a rigid control flow. Other types of expert systems are based on frames, discussed in Chapter 2, and inference nets discussed in Chapter 4.

There are a number of differences between expert systems and conventional programs. Table 1.12 lists some differences.

| Characteristic | Conventional Program | Expert System |
|---|---|---|
| Control by | Statement order | Inference engine |
| Control and data | Implicit integration | Explicit separation |
| Control Strength | Strong | Weak |
| Solution by | Algorithm | Rules and inference |
| Problem search | All or none | Large |
| Input solving | Solution is correct | Rare |
| Input | Assumed correct | Incomplete, incorrect |
| Unexpected input | Difficult to deal with | Very responsive |
| Output | Always correct | Varies with problem |
| Explanation | None | Usually |
| Applications | Numeric, file, and text | Symbolic reasoning |
| Execution | Generally sequential | Opportunistic rules |
| Program design | Structured design | Little or no structure |
| Modifiability | Difficult | Reasonable |
| Expansion | Done in major jumps | Incremental |

Expert systems are normally used to deal with uncertainty. The uncertainty may arise in the input data to the expert system and even the knowledge base itself. At first this may seem surprising to people used to conventional programming. However, much of human knowledge is heuristic, which means that it may only work correctly part of the time so we try something else. In addition, the input data may be incorrect, incomplete, inconsistent, and have other errors. Algorithmic solutions are not capable of dealing with situations like this because an algorithm guarantees the solution of a problem in a finite series of steps.

Depending on the input data and the knowledge base, an expert system may come up with the correct answer, a good answer, a bad answer, or no answer at all. While this may seem shocking at first, the alternative is to have no answer all of the time. Again, the important thing to keep in mind is that a good expert system will perform no worse than the best problem solver for problems like this—a human expert—and may do better. If we knew an efficient algorithmic method that was better than an expert system, we would use it. The important thing is to use the best, and perhaps only, tool for the job.

## Nondeclarative Programming

Nondeclarative paradigms are very popular in PROLOG and SQL. New versions of PROLOG have been developed for AI, and SQL is the standard for relational databases. They are used for a wide variety of applications, from standalone applications or in conjunction with other paradigms.
