+   1. Abstract the application into heterogeneous functional tiers.
+   2. Identify components to carry out finely grained behaviors.
+   3. Create interfaces or glue between the layers.
+   4. Implement the component interfaces and their methods.

From these techniques or principles, it is clear we are following an inductive approach. We start from the general and delve into the details.

# Abstract the Application into Tiers

All useful software is created to solve one or more problems. All problems can always be divided or separated into subproblems. With components, it is important to split large and sophisticated problems into smaller, more manageable ones. By using this divide-and-conquer approach, we ensure that the problem as a whole will be solved and also create a robust and easily maintainable architecture. It is much easier to modify and upgrade a single component consisting of a subproblem than to try to tackle an entire monolithic problem, with the usual retesting and debugging.

# Identify Components

This phase is a little more challenging and requires foresight (and hindsight). It’s probably the most fun and creative phase of all because it brings together past experiences, current technology, and analytical problem solving.

Again, although not all applications can seamlessly fit the three-tiered model, they can always be logically separated into this abstraction at some level.

Start with presentation. Will the application interact with a user via a graphic interface or is it a service that fulfills request blindly? Creating intuitive and user-friendly GUIs is not a trivial task. All too often, you see GUIs that are plagued with inconsistencies from screen to screen or are too busy. This only compounds the problems when you are working with browsers and their lack of rich control sets or state.

You won’t learn GUI design here, but it is worth mentioning that it should not be taken lightly. Remember that although the presentation tier is just the tip of the iceberg, it is the one and only communication link between a user and what constitutes the application. The tiny presentation tier can be sitting on the shoulders of a huge sophisticated business tier, but if it’s not exporting a user-friendly working environment, or is inconsistent, the user might unfairly dismiss the entire application.

![](bbox=[0.876, 0.284, 1.0, 0.434])