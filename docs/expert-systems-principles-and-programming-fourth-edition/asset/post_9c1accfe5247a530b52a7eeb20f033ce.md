

### Figure 1.7 Foundations of Modern Rule-Based Expert Systems

![](img/2c460d4de56b7ffaad3834eee20beaa0_56_0.png)

These figures illustrate the relationship of expert systems to other paradigms and should be considered a general guide rather than strict definitions. In particular, although CLIPS is shown as rule-based, it is possible to write an entirely object-oriented expert system in CLIPS, or a hybrid system using both rules and objects. Some of the paradigms and languages have characteristics that may place them in more than one class. For example, some consider functional programming more, while others consider it declarative.

### Figure 1.8 Procedural Languages

![](img/2c460d4de56b7ffaad3834eee20beaa0_56_1.png)

### Figure 1.9 Nonprocedural Languages

![](img/2c460d4de56b7ffaad3834eee20beaa0_57_0.png)

An algorithm is a method of solving a problem in a finite number of steps. The implementation of an algorithm in a program is a procedural program. The terms algorithmic programming, procedural programming, and conventional programming are often used synonymously to mean non-AI programs. A common conception of a procedural program is that it proceeds sequentially, statement by statement, unless a branch instruction is encountered. Another often used synonym for procedural program is sequential program. However, the term sequential programming implies too much constraint since all modern programming languages support recursion and so programs may not be strictly sequential.

The distinguishing feature of the procedural paradigm is that the programmer must specify exactly how a problem solution must be coded. Even code generators must produce procedural code. In a sense, the use of code generators is non-procedural programming because it removes most or all of the procedural code writing from the programmer. The goal of nonprocedural programming is to have the programmer specify what the goal is and let the system determine how to accomplish it.

## Imperative Programming

The terms imperative and statement-oriented are used synonymously. A language such as C has the dominant characteristic that statements are imperatives or commands to the computer telling it what to do. Note that in an object-oriented version C++, objects may also be used and the general concept is that of objects passing messages to each other. Thus the execution of an object-oriented program is more similar to an event-driven system rather than an imperative one in which program flow is assumed to execute sequentially from beginning to end.

The imperative programming paradigm is an abstraction of real computers which in turn are based on the Turing machine and the von Neumann machine with its registers and store (memory). At the heart of these machines is the concept of a modifiable store. Variables and assignments are the programming language analog of the modifiable store. The store is the object that is manipulated by the program. Imperative programming languages have a rich variety of commands to provide structure to code and to manipulate the store. Each imperative programming language defines a particular view of hardware. These views are so distinct that it is common to speak of a Pascal virtual machine, or a Java virtual machine that executes bytecodes that will execute on any hardware platform. This feature of bytecode portability accounted for much of the success of Pascal in the 1970s and 80s until Java used the same system. In fact, a compiler implements the virtual machine defined by the programming language in the language supported by the actual hardware and operating system.

In imperative programming, a name may be assigned to a value and later re-assigned to another value. The collection of names and the associated values and the location of control in the program constitute the state. The state is a logical model of storage that is an association between memory locations and values. During execution, a program can be characterized as making a transition from the initial state to a final state by passing through a sequence of intermediate states. The transition from one state to the next is determined by assignment operations, input, and sequencing commands.

Imperative languages developed as a way of freeing the programmer from coding assembly language in the von Neumann architecture. Consequently, imperative languages offer great support to variables, assignment operations, and repetition. These are all low-level operations that modern languages attempt to hide by providing features such as recursion, procedures, modules, packages, and so forth. Imperative languages are also characterized by their emphasis on rigid control structure and their associated top-down program designs.

A serious problem with all languages is the difficulty of proving the correctness of programs which means the program is valid (discussed more in Chapter 2). From the AI standpoint, another serious problem is that imperative languages are not very efficient symbol manipulators. Because the imperative language architecture was molded to fit the von Neumann computer architecture, we have languages that can support number-crunching very well but not symbolic manipulation. However, imperative languages such as C and object-oriented languages such as C++ and Java have been used as the underlying base language to write expert system shells. These languages and the shells built from them run more efficiently and quickly on common general-purpose computers than the early shells built using LISP that required special hardware expressly designed for LISP.

Because of their sequential nature, imperative languages are not very efficient for directly implementing expert systems, especially rule-based ones. As an illustration of this problem, consider the task of encoding the information of a real-world problem with hundreds or thousands of rules. For example, the classic XCON system used to configure computer systems had about 7000 rules in its knowledge base. Early unsuccessful attempts were made to code this program in FORTRAN and BASIC before settling on the successful expert systems approach. An expert system tool like CLIPS makes it much easier to create such a large rule base than programming in a 3rd generation language or object-oriented language like Java, C++, or C#. To fully appreciate the advantages of an expert system language, you need to try coding in it. Programming in CLIPS is covered in the second part of this book.

The direct way of coding this knowledge in an imperative language would require 7000 IF-THEN statements or a very, very long CASE. This style of coding would present major efficiency problems since all 7000 rules would need to be searched for matching patterns on every recognize–act cycle. Note that the inference engine and its recognize–act cycle would also have to be coded in the imperative language. However the situation is much more complex than merely writing 7000 rules since many of the rules are triggered by other rules. For example, in the case of stopping for a red light, this would only apply if you were approaching the light; not if you had passed it. Many other interactions are possible in a rule-based system. Some rules assert facts, some may retract facts, some may modify facts. More sophisticated rules may create new rules or delete rules in the case of machine learning.

The efficiency of the program could be improved if rules were ordered so that those most likely to be executed were put at the beginning. However, this would require considerable tuning of the system and would change as new rules are added, or old ones deleted and modified. A better method for improving efficiency would be to build a dynamic network in memory of the rule patterns to reduce search time in determining which rules should be activated. Rather than making the programmer manually construct the tree, it should preferably be built automatically by the computer, based on the pattern and action syntax of the IF-THEN rules. It would also be helpful to have an IF-THEN syntax that was more conducive to representing knowledge and had powerful pattern matching tests. This requires the development of a parser to analyze input structure and an interpreter or compiler to execute the new IF-THEN syntax.

When all of these techniques for improving efficiency are implemented, the result is a dedicated expert system. If the inference engine, parser, and interpreter are removed to provide easy development of other expert systems, they compose an expert system shell. Of course, instead of doing all of this development from scratch, today it is much easier to use an existing tool like CLIPS, that is well-documented and extensively tested.

## Functional Programming

The nature of **functional programming**, as exemplified by languages such as LISP, is very different from statement-oriented languages with their heavy reliance on elaborate control structures and top-down design. Conventional languages place conceptual limits on the way problems can be modularized. Functional languages push those limits back. Two features of functional languages in particular, higher-order functions and lazy evaluation, can contribute greatly to modularity. The fundamental idea of functional programming is to combine simple functions to yield more powerful functions. This is essentially a **bottom-up** design in contrast to the common **top-down** designs of imperative languages.

Functional programming is centered around **functions**. Mathematically, a function is an **association** or rule that maps members of one set, the **domain**, into another set, the **codomain**. The following is an example of a function definition:

```
cube(x) == x**3, where x is a real number and
cube is a function with real values
```

