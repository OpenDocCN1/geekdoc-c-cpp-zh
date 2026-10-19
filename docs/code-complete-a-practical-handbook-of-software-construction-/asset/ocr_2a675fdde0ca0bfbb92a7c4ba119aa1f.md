# Classes to Avoid

While classes in general are good, you can run into a few gotchas. Here are some classes to avoid.

**Package related operations** In cases in which you can’t hide information, share data, or plan for flexibility, you can still package sets of operations into sensible groups, such as trig functions, statistical functions, string-manipulation routines, bit-manipulation routines, graphics routines, and so on. Classes are one means of combining related operations. You could also use packages, namespaces, or header files, depending on the language you’re working in.

**Accomplish a specific refactoring** Many of the specific refactorings described in Chapter 24, “Refactoring,” result in new classes—including converting one class to two, hiding a delegate, removing a middle man, and introducing an extension class. These new classes could be motivated by a desire to better accomplish any of the objectives described throughout this section.

**Avoid creating god classes** Avoid creating omniscient classes that are all-knowing and all-powerful. If a class spends its time retrieving data from other classes using Get() and Set() routines (that is, digging into their business and telling them what to do), ask whether that functionality might better be organized into those other classes rather than into the god class (Riel 1996).

Cross-Reference This kind of class is usually called a structure. For more on structures, see Section 13.1, “Structures.”

**Eliminate irrelevant classes** If a class consists only of data but no behavior, ask yourself whether it’s really a class and consider demoting it so that its member data just becomes attributes of one or more other classes.

**Avoid classes named after verbs** A class that has only behavior but no data is generally not really a class. Consider turning a class like DatabaseInitialization() or StringBuilder() into a routine on some other class.

# Summary of Reasons to Create a Class

Here’s a summary list of the valid reasons to create a class:

+   - Model real-world objects
+   - Model abstract objects
+   - Reduce complexity
+   - Isolate complexity
+   - Hide implementation details
+   - Limit effects of changes
+   - Hide global data