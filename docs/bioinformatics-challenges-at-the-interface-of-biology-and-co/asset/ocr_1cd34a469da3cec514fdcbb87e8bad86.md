# Table 6.5

How common programming languages relate to the four paradigms of algorithm design: imperative, functional, logic and object-oriented. For a given language, a paradigm may be ✓ exemplified (the language was designed around it), ✓ supported (the language provides mechanisms for its use), or effectively unsupported if left blank.

| Language | Imperative | Functional | Logic | Object-oriented |
| :--- | :---: | :---: | :---: | :---: |
| C | ✓ | | | |
| C++ | ✓ | | | ✓ |
| Haskell | | ✓ | | |
| Java | ✓ | | | |
| JavaScript | | (✓) | | ✓ |
| Lisp | | | ✓ | |
| Oz | | | | | |
| Perl | ✓ | | | ✓ |
| Prolog | | | ✓ | |
| Python | ✓ | (✓) | | ✓ |
| Ruby | ✓ | (✓) | | ✓ |

although the same doesn't necessarily hold for the choice of programming language (see Section 6.6.2). Having said, paradigmatic choice is not without consequences. Which paradigm we choose – if a choice exists – depends on the nature of the problem, from which it's often evident which paradigm is the best fit: if the problem concerns interdependent state agents, object-oriented is likely to be the appropriate choice; if it involves logically proving or disproving a set of mathematical rules, logic programming is likely to fit better.

By 'better', we mean a number of immediate gains: choosing the correct paradigm can drastically speed development time, make code smaller, and allow it to run more efficiently. However, there are other reasons for choosing one paradigm over another; for example, some methods of optimisation are more easily implemented in some paradigms than others (see Section 6.6.4 for an example of this).

# Paradigmatic reality

For worse, software-engineering courses tend to concentrate on imperative and object-oriented software development, and the most common languages in use follow those paradigms. Consequently in many cases might be ideal, imperative languages have been used to solve functional or logical problems – this clearly be seen by the rise in availability of such things as anonymous functions (the building-blocks of the functional paradigm) in imperative languages. On the one hand, for many users, the benefit of being able to code in multiple paradigms within the same code gives developers greater flexibility in how they can express their thoughts; although mixed-paradigm languages are becoming more abundant, they aren't necessarily the most efficient way of implementing these paradigms; there is potential for them to be 'Jack of all paradigms, master of none'. These issues, and the need to support or build legacy software, will inform (or restrict) the developer's choice.