# 84. Prefer algorithm calls to handwritten loops.

**Summary**

Use function objects judiciously: For very simple loops, handwritten loops can be the simplest and most efficient solution. But writing algorithm calls instead of handwritten loops can be more expressive and maintainable, less error-prone, and as efficient.

When calling algorithms, consider writing your own custom function object that encapsulates the logic you need. Avoid cobbling together parameter-binders and simple function objects (e.g., `bind2nd`, `plus`), which usually degrade clarity. Consider trying the [Boost] Lambda library, which automates the task of writing function objects.

**Discussion**

Programs that use the STL tend to have fewer explicit loops than non-STL programs, replacing low-level semantics-free loops with higher-level and better-defined abstract operations that convey greater semantic information. Prefer a "process this range" algorithmic mindset over "process each element" loopy thinking.

A primary benefit that algorithms and design patterns have in common is that they let us speak at a higher level of abstraction with a known vocabulary. These days, we don't say "let many objects watch one object and get automatic notifications when its state changes;" rather, we say just "Observer." Similarly, we say "Bridge," "Factory," and "Visitor." Our shared pattern vocabulary raises the level, effectiveness, and correctness of our discussion. With algorithms, we likewise don't say "perform an action on each element in a range and write the results somewhere;" rather, we say *transform*. Similarly, we say *for_each*, *replace if*, and *partition*. Algorithms, like design patterns, are self-documenting. Naked *for* and *while* loops just don't do it when it comes to imparting any inherent semantic information about the purpose of the loop; they force readers to inspect their loop bodies to decipher what's going on.

Algorithms are also more likely to be correct than loops. Handwritten loops easily make mistakes such as using invalidated iterators (see Items 83 and 99); algorithms come already debugged for iterator invalidation and other common errors.

Finally, algorithms are also often more efficient than naked loops (see [Sutter00] and [Meyers01]). They avoid needless minor inefficiencies, such as repeated evaluations of `container.end()`. Slightly more importantly, the standard algorithms you're using were implemented by the same people who implemented the standard containers you're using, and by dint of their inside knowledge those people can write algorithms that are more efficient than any version you would write. Most important of all, however, is that many algorithms have highly sophisticated implementations that we in-the-trenches programmers are unlikely ever to match in handwritten code (unless we don't need the full generality of everything a given algorithm does).