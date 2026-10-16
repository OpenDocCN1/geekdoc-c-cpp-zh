# Adding Objects

Fundamentally speaking, all software development technologies are ultimately aimed at solving one specific problem. The problem is that thinking about more than one idea at a time is difficult for human beings. So, all these technologies enable us to compartmentalize and encapsulate our ideas into reusable packages that can be mixed and matched in novel ways to solve new problems.

You’ve already seen how procedural programming — breaking our ideas out into procedures that we can reuse — enables exactly this kind of compartmentalization and encapsulation. Procedural programming was a revolutionary concept when it was initially introduced early in computer science history. However, it had one major flaw: Procedures have no mechanism for storing state within themselves. Typically, procedural programmers work around this limitation by either passing state variables into the procedures along with the parameters that are necessary for the procedure to do its work, or by relying on global variables to store their state instead. Both of these are not ideal solutions.

Passing state variables into the procedures can quickly get out of hand because, as your programs become more complex, they require more and more state to be preserved between procedure calls.

Using global variables is similarly complicated because excessive use of global variables can lead to excessive dependencies that are difficult to track in your code. For example, to determine what global variables a particular procedure relies on, you have to become familiar with the procedure itself. There’s no way to know simply by looking at the interface of a procedure what global variables that particular procedure relies upon. This leads to variables not being initialized properly, or side effects, such as variables receiving values that you were not aware were accessed in that function.

As procedural applications became more and more complicated, these problems became more insurmountable by developers.

# In This Chapter

+   - Learning object-oriented terminology
+   - Working with objects in Objective-C
+   - Creating classes and class hierarchies
+   - Defining properties
+   - Writing class and object methods
+   - Declaring member variables