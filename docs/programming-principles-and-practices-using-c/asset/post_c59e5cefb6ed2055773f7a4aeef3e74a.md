
an embedded system involving hard real-time constraints or for a system needing to run "forever" may prohibit the use of `new`. Typically, a coding standard also tries to ensure that code written by two programmers is more similar than if they had chosen freely from all possible styles. For example, a coding standard may require that `for`-statements be used for loops (thereby banning `while`-statements). This can make code more uniform, and in large projects that can be important for maintenance. Please note that a coding standard is aimed at improving code for a specific kind of programming given a specific kind of programmer. There is no one coding standard suitable for all C++ applications and all C++ programmers.

So, the problems that a coding standard tries to address are problems that arise from the way we express our solutions rather than the problems that arise from inherent complexities of the problem we are trying to solve with our application. We could say that coding standards are trying to address incidental complexities rather than inherent complexities.

The major sources of such incidental complexities are:

- *Overly clever programmers*, who use features they don't understand or delight in complicated solutions
- *Undereducated programmers*, who don't use the most appropriate language and library features
- *Unnecessary variations in programming style*, causing code performing similar tasks to look different and confuse maintainers
- *Inappropriate programming language*, leading to use of language features that are poorly adapted to a particular application area or to a particular group of programmers
- *Insufficient library use*, leading to lots of ad hoc manipulation of low-level resources
- *Inappropriate coding standards*, causing extra work or prohibiting the best solution to some classes of problems, thus becoming a source of the kind of problems that the standards were introduced to solve

### 25.6.1 What should a coding standard be?

A good coding standard should help a programmer write good code; that is, it should help the programmer by giving answers to lots of little questions that each programmer would otherwise have to spend time deciding on a case-by-case basis. There is an old engineer's proverb that says, "Form is liberating." Ideally, a coding standard should be prescriptive, stating what should be done. That seems obvious, but many coding standards are simply a list of prohibitions, with no guidance about what to do after having obeyed a long list of *don'ts*. Just being told what not to do is rarely helpful and often annoying.

The rules of a good coding standard should be verifiable, preferably by a program; that is, once we have written the code, we should be able to look at it and easily answer the question, "Have I broken any rule of my coding standard?"

A good coding standard should present a rationale for the rules. Programmers should not just be told, "Because that's the way we do it!" When they are, they resent it. Worse, programmers invariably try to subvert parts of a coding standard that they see as pointless and as preventing them from doing a good job. Don't expect to like everything about a coding standard. Even the best coding standard is a compromise, and most prohibit certain practices assumed to cause problems – even if they never caused you a problem. For example, inconsistent naming rules are a source of confusion, but different people have strong attachments to some naming conventions and strong dislikes of others. For example, I consider the CamelCodingStyle of identifiers "ugly" and strongly prefer `underscore_style` as cleaner and inherently more readable, and many people agree. On the other hand, many reasonable people disagree. Obviously, no naming standard can please everyone, but in this case, as in many others, a consistent style is definitely better than the lack of a standard.

To summarize:

- A good coding standard is designed for a specific application domain and a specific group of programmers.
- A good coding standard is prescriptive as well as restrictive.
  - Recommending some "foundation" library facilities is often the most effective use of prescriptive rules.
- A coding standard is a set of rules for what code should look like,
  - Typically specifying naming and indentation rules; e.g., "Use 'Stroustrup layout.'"
  - Typically specifying a subset of a language; e.g., "Don't use new or throw."
  - Typically specifying rules for commenting; e.g., "Every function must have a comment explaining what it does."
  - Often requiring the use of certain libraries; e.g., "Use `<iostream>` rather than `<stdio.h>`" or "Use vector and string rather than built-in arrays and C-style strings."
- Common aims of most coding standards are to improve:
  - Reliability
  - Portability
  - Maintainability
  - Testability
  - Reusability
  - Extensibility
  - Readability
- A good coding standard is better than no standard. We wouldn’t start a major (multi-person, multi-year) industrial project without one.
- A poor coding standard can be worse than no standard. For example, C++ coding standards that restrict programming to something like the C subset do harm. Unfortunately, poor coding standards are not uncommon.
- All coding standards are disliked by programmers, even the good ones. Most programmers want to write their code exactly the way they like it.

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_1009_0.png)

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_1009_1.png)

### 25.6.2 Sample rules

Here, we would like to give you a flavor of a coding standard by listing some rules. Naturally, we pick rules that we hope will be useful to you. However, we have never seen a real-world coding standard that could be described in fewer than 35 pages, and most are much longer. So, we don’t try to give you a complete set of rules here. Furthermore, every good coding standard is designed for a particular application area and for a particular set of programmers. So, we don’t make any pretenses of universality.

The rules are numbered and contain a (brief) rationale. Many rules contain examples for easier comprehension. We distinguish between *recommendations*, which a programmer may occasionally decide to ignore, and *firm rules*, which must be followed. In a real set of rules, a firm rule can usually be broken (only) with written permission from a supervisor. Each violation of a recommendation or a firm rule requires a comment in the code. Any exceptions to a rule can be listed in the rule. A firm rule is identified by a capital R in its number. A recommendation is identified by a lowercase r in its number.

The rules are classified as:

- General
- Preprocessor
- Naming and layout
- Class rules
- Function and expression rules
- Hard real time
- Critical systems

The “hard real-time” and “critical systems” rules apply only to projects classified as such.

Compared to a good real-world coding standard, our terminology is under-specified (e.g., what does “critical” really mean?) and the rules overly terse. Similarities between these rules and the JSF++ rules (see [25.6.3]) are not accidental; I helped formulate the JSF++ rules. However, the code examples in this book do not conform to the rules below – after all, the book code is not critical embedded systems code.

#### General rules

- **R100:** Any one function or class shall contain no more than 200 logical source lines of code (non-comments).
  - *Reason:* Long functions and long classes tend to be complex and therefore difficult to comprehend and test.

- **r101:** Any one function or class should fit on a screen and serve a single logical purpose.
  - *Reason:* A programmer looking at only part of a function or class is more likely to overlook a problem. A function that tries to perform several logical functions is likely to be longer and more complex than one that doesn’t.

- **R102:** All code shall conform to ISO/IEC 14882:2011 (E) standard C++.
  - *Reason:* Language extensions or variations from ISO/IEC 14882 are likely to be less stable, to be less well specified, and to limit portability.

#### Preprocessor rules

- **R200:** No macros shall be used except for source control using `#ifdef` and `#ifndef`.
  - *Reason:* Macros don’t obey scope and type rules. Macro use is not obvious when visually examining source text.

- **R201:** `#include` shall be used only to include header (*.h) files.
  - *Reason:* `#include` is used to access interface declarations – not implementation details.

- **R202:** All `#include` directives shall precede all non-preprocessor declarations.
  - *Reason:* An `#include` in the middle of a file is more likely to be overlooked by a reader and to cause inconsistencies from a name resolved differently in different places.

- **R203:** Header files (*.h) shall not contain non-const variable definitions or non-inline, non-template function definitions.
