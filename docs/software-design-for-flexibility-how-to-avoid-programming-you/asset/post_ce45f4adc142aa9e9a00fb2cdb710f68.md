
Guy L. Steele Jr.
Lexington, Massachusetts
August 2020

# Preface

We have all spent too much time trying to deform an old piece of code so that it could be used in a way that we didn't realize would be needed when we wrote it. This is a terrible waste of time and effort. Unfortunately, there are many pressures on us to write code that works very well for a very specific purpose, with few reusable parts. But we think that this is not necessary.

It is hard to build systems that have acceptable behavior over a larger class of situations than was anticipated by their designers. The best systems are evolvable: they can be adapted to new situations with only minor modification. How can we design systems that are flexible in this way?

It would be nice if we all had to add a new feature to a program was to add some code, without changing the existing code base. We can often do this by using certain organizing principles in the construction of the code base and incorporating appropriate hooks at that time.

Observations of biological systems tell us a great deal about how to make flexible and evolvable systems. Techniques originally developed in support of symbolic artificial intelligence can be viewed as ways of enhancing flexibility and adaptability in programs and other engineered systems. By contrast, common practice of computer science actively discourages the construction of systems that are easily modified for use in novel settings.

We have often programmed ourselves into corners and had to expend great effort refactoring code to escape from those corners. We have now accumulated enough experience to feel that we can identify, isolate, and demonstrate strategies and techniques that we have found to be effective for building large systems that can be adapted for purposes that were not anticipated in the original design.

In this book we share some of the fruits of our over 100 years of programming experience.

# This book

This book was developed as the result of teaching computer programming at MIT. We started this class many years ago, intending to expose advanced undergraduate students and graduate students to techniques and technologies that are useful in the construction of programs that are central to artificial intelligence applications, such as mathematical symbolic manipulation and rule-based systems. We wanted the students to be able to build these systems flexibly, so that it be easier to combine such systems to make even more powerful systems. We also wanted to teach students about dependencies—how they can be tracked, and how they can be used for explanation and to control backtracking.

Although the class was and is successful, it turned out that in the beginning we did not have much understanding of the material as we originally believed. We put a great deal of effort into sharpening our tools and making our ideas more precise. We realize that these techniques are not just for artificial intelligence applications. We think that anyone who is building complex systems, such as computer-language compilers and integrated development environments, will benefit from our experience. This book is built on the lectures and problem sets that are now used in our class.

# The contents

There is much more material in this book than can be covered in a single-semester class. So each time we offer the class we pick and choose what to present. Chapter 1 is an introduction to our programming philosophy. Here we show *flexibility* in the grand context of nature and of engineering. We try to make the point that flexibility is as important an issue as efficiency and correctness. In each subsequent chapter introduce techniques and illustrate them with sets of exercises. This is an important organizing principle for the book.

In chapter 2 we explore some universally applicable ways of building systems with room to grow. A powerful way to organize a flexible system is to build it as an assembly of domain-specific languages, each appropriate for easily expressing the construction of a subsystem. Here we develop basic tools for the development of domain-specific languages: we show how subsystems can be organized around mix-and-match parts, how they can be flexibly combined with combinators, how wrappers can be used to generalize parts, and how we can often simplify a program by abstracting out a domain model.

In chapter 3 we introduce the extremely powerful but potentially dangerous flexibility technique of predicate-dispatched generic procedures. We start by generalizing arithmetic to symbolic algebraic expressions. We show how such a generalization can be made efficient by using type tags for data, and we demonstrate the power of the technique with the design of a simple, but easy to elaborate, adventure game.

In chapter 4 we introduce symbolic pattern matching, first to enable term-rewriting systems, and later, with unification, to show how type inference can easily be made to work. Here we encounter the need for backtracking because of segment variables. Unification is the first place where we see the power of representing and combining partial-information structures. We end the chapter with extending the idea to matching general graphs.

In chapter 5 we explore the power of interpretation and compilation. We believe that programmers should know how to escape the confines of whatever programming language they must by making an interpreter for a language that is more appropriate for expressing the solution to the current problem. We also show how to naturally incorporate backtracking search by implementing nondeterministic amb in an interpreter/compiler system, and how to use continuations.

In chapter 6 we show how to make systems of layered data and layered procedures, where each data item can be annotated with a variety of metadata. The processing of the underlying data is not affected by the metadata, and the code for processing the underlying data does not even know about or reference the metadata. However, the metadata is processed by its own procedures, effectively in parallel with the data. We illustrate this by attaching units to numerical quantities and by showing how to carry dependency information, giving the provenance of data, as derived from the primitive sources.

This is all brought together in chapter 7, where we introduce propagation to escape the expression-oriented paradigm of computer languages. Here we have a wiring-diagram vision of connecting modules together. This allows the flexible incorporation of multiple sources of partial information.

# Scheme

The code in this book is written in Scheme, a mostly functional language that is a variant of Lisp. Although Scheme is not a popular language, or widely used in an industrial context, it is the right choice for this book.¹

The purpose of this book is the presentation and explanation of programming ideas. The presentation of example code to elucidate these ideas is shorter and simpler in Scheme than in other languages, for many reasons. Languages other than those in the Lisp family require lots of ceremony to say simple things. The only thing that makes our code longwinded is that we tend to use long descriptive names for computational objects.

It is important that Scheme is a permissive rather than a normative language. It does not try to prevent a programmer from doing something "stupid." This allows us to play powerful games, like dynamically modulating the meanings of arithmetic operators. We would not be able to do this in a language that imposes restrictive rules.

Scheme allows assignment but encourages functional programming. Scheme does not have static types, but it has very strong dynamic typing that allows safe dynamic storage allocation and garbage collection: a user program cannot manufacture a pointer or access an arbitrary memory location. It is not that we think static types are not a good idea. They certainly are useful for the early exorcism of a large class of bugs. And Haskell-like type systems can be helpful in thinking out strategies. But for this book the intellectual overhead of static types would inhibit consideration of potentially dangerous strategies of flexibility.

Also Scheme provides special features, such as reified continuations and dynamic binding, that are not available in most other languages. These features allow us to implement such powerful mechanisms as nondeterministic amb in the native language (without a second layer of interpretation).

¹ We provide a short introduction to Scheme in Appendix B.
