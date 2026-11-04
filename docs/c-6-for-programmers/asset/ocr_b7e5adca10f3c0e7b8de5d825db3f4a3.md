their styles to "goto-less programming." The term structured programming became almost synonymous with "goto elimination." Not until the 1970s did most programmers start taking structured programming seriously. The results were impressive. Software development groups reported shorter development times, more frequent on-time delivery of systems and more frequent within-budget completion of software projects. The key to these successes was that structured programs were clearer, easier to debug and modify, and more likely to be bug free in the first place.

Bohm and Jacopini's work demonstrated that all programs could be written in terms of only three control structures—the sequence structure, the selection structure and the iteration structure. We'll discuss how each of these is implemented in C#.

# 5.2.1 Sequence Structure

The sequence structure is built into C#. Unless directed otherwise, C# statements execute one after the other in the order in which they're written—that is, in sequence. The UML activity diagram in Fig. 5.1 illustrates a typical sequence structure in which two calculations are performed in order. C# lets you have as many actions as you want in a sequence structure.

![](bbox=[0.12, 0.6, 0.9, 0.72])

Fig. 5.1 | Sequence structure activity diagram.

An activity diagram models the workflow (also called the activity) of a portion of a software system. Such workflows may include a portion of an algorithm, like the sequence structure in Fig. 5.1. Activity diagrams are composed of symbols, such as

+   - action-state symbols (rectangles with their left and right sides replaced with outward arcs),
+   - diamonds and
+   - small circles.

These symbols are connected by transition arrows, which represent the flow of the activity—that is, the order in which the actions should occur.

1. C. Bohm and G. Jacopini, "Flow Diagrams, Turing Machines, and Languages with Only Two Formation Rules," Communications of the ACM, Vol. 9, No. 5, May 1966, pp. 336–371.