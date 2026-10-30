This is a useful analogy in programming, too. Skyhooks are indicative of a deeper problem. All skyhooks should be replaced with appropriate cranes.

The presence of a skyhook in code is difficult to replace with a fake implementation, thereby reducing testability. Examples of skyhooks are:

+   - Static methods
+   - Static classes (including singletons)
+   - Object construction that uses new
+   - Extension methods

Each of these make testing more difficult! by hindering your ability to inject mocks into your code; they are skyhooks and thus they are undesirable. Each is used ex nihilo—from nothing.

Luckily, each of these can be replaced with a suitable crane, such as the following, that will facilitate some kind of external injection (that is, it can be used ex materia—from something):

+   - Interfaces
+   - Dependency injection
+   - Inversion of control
+   - Factories

In subsequent chapters of this book, each of these "cranes" of programming is explained in more detail.

# Metrics

Source code has been subject to many different metrics through the years, each of which attempts to reduce the complexity of code down to numbers that indicate the health—or otherwise—of the project as a whole.

This might seem rather reductive, but metrics have evolved somewhat since middle-management obsessed over source lines of code (SLOC). Although SLOC correlates well to the effort required—it takes longer to write more lines of code than it does to write fewer—it does not necessarily correlate to the level of functionality of a system. Nor, indeed, is it a reliable measure of a developer's productivity.