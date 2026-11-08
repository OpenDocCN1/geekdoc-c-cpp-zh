+   3. Remove duplication.
+   4. Decrease elements.

The numbers are both the order in which these are executed and the priority they are given.

Point 1 is self-evident. The code must pass all the tests. The code must work.

Point 2 says that after the code is made to work, it should then be made expressive. It should reveal the intention of the programmer. It should be easy to read and self-descriptive. This is where we apply many of the simpler and more cosmetic refactorings. We also split large functions into smaller, better-named functions.

Point 3 says that after we have made the code as descriptive and expressive as possible, we hunt for and remove any duplication within that code. We don’t want the code to say the same thing more than once. During this activity, the refactorings are usually more complicated. Sometimes removing duplication is as simple as moving the duplicate code into a function and calling it from many places. Other times it requires more interesting solutions, such as the Design Patterns:⁴ *Template Method, Strategy, Decorator,* or *Visitor*.

Point 4 says that once we have removed all the duplication, we should strive to decrease the number of structural elements, such as classes, functions, variables, etc.

The goal of Simple Design is to keep the *design weight* of the code as small as practicable.

⁴ Design Patterns are beyond the scope of this book. See Gamma, E., R. Helm, R. Johnson, and J. Vlissides. 1995. *Design Patterns: Elements of Reusable Object-Oriented Software*. Reading, MA: Addison-Wesley.