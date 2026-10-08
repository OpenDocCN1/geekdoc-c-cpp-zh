
## 22.1.2.1 What we want

Typically, we want:

- **Correctness**: Yes, it can be difficult to define what we mean by “correct,” but doing so is an important part of the complete job. Often, others define for us what is correct for a given project, but then we have to interpret what they say.
- **Maintainability**: Every successful program will be changed over time; it will be ported to new hardware and software platforms, it will be extended with new facilities, and new bugs will be found that must be fixed. The sections below about ideals for program structure address this ideal.
- **Performance**: Performance (“efficiency”) is a relative term. Performance has to be adequate for the program’s purpose. It is often claimed that efficient code is necessarily low-level and that concerns with a good, high-level structure of the code cause inefficiency. On the contrary, we find that acceptable performance is often achieved through adherence to the ideals and approaches we recommend. The STL is an example of code that is simultaneously abstract and very efficient. Poor performance can as easily arise from an obsession with low-level details as it can from disdain for such details.
- **On-time delivery**: Delivering the perfect program a year late is usually not good enough. Obviously, people expect the impossible, but we need to deliver quality software in a reasonable time. There is a myth that “completed on time” implies shoddiness. On the contrary, we find that emphasis on good structure (e.g., resource management, invariants, and interface design), design for testability, and use of appropriate libraries (often designed for a specific application or application area) is a good way to meet deadlines.

This leads to a concern for structure in our code:

- If there is a bug in a program (and every large program has bugs), it is easier to find in a program with a clear structure.
- If a program needs to be understood by a new person or needs to be modified in some way, a clear structure is comprehensible with far less effort than a mess of low-level details.
- If a program hits a performance problem, it is often easier to tune a high-level program (one that is a good approximation of the ideals and has a well-defined structure) than a low-level or messy one. For starters, the high-level one is more likely to be understandable. Second, the high-level one is often ready for testing and tuning long before the low-level one.

Note the point about a program being understandable. Anything that helps us understand a program and helps us reason about it is good. Fundamentally, regularity is better than irregularity — as long as the regularity is not achieved through oversimplification.

## 22.1.2.2 General approaches

There are two approaches to writing correct software:

- **Bottom-up**: Compose the system using only components proved to be correct.
- **Top-down**: Compose the system out of components assumed to contain errors and catch all errors.

Interestingly, the most reliable systems combine these two — apparently contrary — approaches. The reason for that is simple: for a large real-world system, neither approach will deliver the needed correctness, adaptability, and maintainability:

- We can't build and “prove” enough basic components to eliminate all sources of errors.
- We can't completely compensate for the flaws of buggy basic components (libraries, subsystems, class hierarchies, etc.) when combining them in the final system.

However, a combination of approximations to the two approaches can deliver more than either in isolation: we can produce (or borrow or buy) components that are sufficiently good, so that the problems that remain can be compensated for by error handling and systematic testing. Also, if we keep building better components, a larger part of a system can be constructed from them, reducing the amount of “messy ad hoc code” needed.

Testing is an essential part of software development. It is discussed in some detail in Chapter 26. Testing is the systematic search for errors. “Test early and often” is a popular slogan. We try to design our programs to simplify testing and to make it harder for errors to “hide” in messy code.

## 22.1.2.3 Direct expression of ideas

When we express something — be it high-level or low-level — the ideal is to express it directly in code, rather than through work-arounds. The fundamental ideal of representing our ideas directly in code has a few specific variants:

- **Represent ideas directly in code.** For example, it is better to represent an argument as a specific type (e.g., Month or Color) than as a more general one (e.g., int).
- **Represent independent ideas independently in code.** For example, with a few exceptions, the standard `sort()` can sort any standard container of any element type; the concepts of sorting, sorting criteria, container, and element type are independent. Had we built a `vector` of objects allocated on the free store where the elements are of a class derived from **Object** with a `before()` member function defined for use by `vector::sort()`, we would have a far less general `sort()` because we made assumptions about storage, class hierarchy, available member functions, ordering, etc.
- **Represent relationships among ideas directly in code.** The most common relationships that can be directly represented are inheritance (e.g., a **Circle** is a kind of **Shape**) and parameterization (e.g., a `vector<T>` represents what's common for all vectors independently of a particular element type).
- **Combine ideas expressed in code freely – where and only where combinations make sense.** For example, `sort()` allows us to use a variety of element types and a variety of containers, but the elements must support `<` (if they do not, we use the `sort()` with an extra argument specifying the comparison criteria), and the containers we sort must support random-access iterators.
- **Express simple ideas simply.** Following the ideals listed above can lead to overly general code. For example, we may end up with class hierarchies with a more complicated taxonomy (inheritance structure) than anyone needs or with seven parameters to every (apparently) simple class. To avoid every user having to face every possible complication, we try to provide simple versions that deal with the most common or most important cases. For example, we have a `sort(b,e)` that implicitly sorts using less than in addition to the general version `sort(b,e,op)` that sorts using `op`. We could also provide versions `sort(c)` for sorting a standard container using less than and `sort(c,op)` for sorting a standard container using `op`.

## 22.1.2.4 Abstraction level

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_844_0.png)

For example, consider how to represent entries for a phone book (as we might keep it on a PDA or a cell phone). We could represent a set of (name,value) pairs as a `vector<pair<string,Value_type>>`. However, if we essentially always accessed that set using a name, `map<string,Value_type>` would be a higher level of abstraction, saving us the bother of writing (and debugging) access functions. On the other hand, `vector<pair<string,Value_type>>` is itself a higher level of abstraction than two arrays, `string[max]` and `Value_type[max]`, where the relationship between the string and its value is implicit. The lowest level of abstraction would be something like an `int` (number of elements) plus two `void*`s (pointing to some form of representation, known to the programmer but not to the compiler). In our example, every suggestion so far could be seen as too low-level because it focuses on the representation of the pair of values, rather than their function. We could move closer to the application by defining a class that directly reflects a use. For example, we could write our application code using a class `Phonebook` with an interface designed for convenient use. That `Phonebook` class could be implemented using any one of the representations suggested.

The reason for preferring the higher level of abstraction (when we have an appropriate abstraction mechanism and if our language supports it with acceptable efficiency) is that such formulations are closer to the way we think about our problems and solutions than solutions that have been expressed at the level of computer hardware.

The reason given for dropping to a lower level of abstraction is typically “efficiency.” This should be done only when really needed (§25.2.2). Using a lower-level (more primitive) language feature does not necessarily give better performance. Sometimes, it eliminates optimization opportunities. For example, using a `Phonebook` class, we have a choice of implementations, say, between `string[max]` plus `Value_type[max]` and `map<string,Value_type>`. For some applications the former is more efficient and for others the latter is. Naturally, performance would not be a major concern in an application involving only your personal directory. However, this kind of trade-off becomes interesting when we have to keep track of – and manipulate – millions of entries. More seriously, after a while, the use of low-level features soaks up the programmer’s time so that opportunities for improvements (performance or otherwise) are missed because of lack of time.

## 22.1.2.5 Modularity

Modularity is an ideal. We want to compose our systems out of “components” (functions, classes, class hierarchies, libraries, etc.) that we can build, understand, and test in isolation. Ideally, we also want to design and implement such components so that they can be used in more than one program (“reused”). *Reuse* is the building of systems out of previously tested components that have been used elsewhere – and the design and use of such components. We have touched upon this in our discussions of classes, class hierarchies, interface design, and generic programming. Much of what we say about “programming styles” (in §22.1.3) relates to the design, implementation, and use of potentially “reusable” components. Please note that not every component can be used in more than one program; some code is simply too specialized and is not easily improved to be usable elsewhere.

Modularity in code should reflect important logical distinctions in the application. We do not “increase reuse” simply by putting two completely separate
