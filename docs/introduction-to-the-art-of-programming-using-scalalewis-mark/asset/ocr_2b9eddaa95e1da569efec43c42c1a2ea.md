# 27.2 Refactorings

Fowler’s book on refactoring lists 72 different refactoring methods. Only a few will be discussed here. Not only should interested readers turn to the original book for a full description, many of the refactoring methods presented in the book involve concepts that are beyond the scope of this book or what the reader is expected to understand at this point in his/her Computer Science education.

# 27.2.1 Built-in Refactoring Methods

Many of the refactoring methods are algorithmic in nature. For this reason, Integrated Development Environments (IDEs), such as Eclipse, have a number of them written in. Using built-in refactoring tools can make things go much faster. They are also set up so that they have no impact on the behavior of the code. They change the structure without changing the functionality.

As of this writing, the following options are available under the refactoring menu when you right click on code in Eclipse under Scala.³

+   - Rename - This can be applied to any programmer given name such as variable names, method names, or class names. Just as comments that no longer fit the code are smelly, using names in your programs that are hard to understand or, worst yet, are misleading, should have you detecting a rank stench. Of course, you can change the name of something on your own, but that means finding all the places it is used and changing them as well. For something like the name of a public method in a large project, this can mean tracking down invocations in many different files. This refactoring option does all that for you. So if you find that a name you chose early in the development of a project no longer fits, select this option and change it to something that does.
+   - Inline Local - This will remove a local val and change all references to it to the value it is initialized to. This should only be done with immutable values as this operation can change behavior if the object is mutated in some of the usages. You would use this if you put something in a variable expecting it would be long or used many times and then come to find out neither is true.
+   - Organize Imports - This very handy option, which has the keystroke Ctrl-Alt-O, will automatically add imports for any types that are lacking them. It also organizes the import statements at the top of the file. It should be noted that this uses Java-style imports that go at the top of the file and have one class per line. If you need an import to be local, you should add that yourself. The fact that it uses a longer format is not that important as you do not have to type it.
+   - Extract Local - This is the inverse of Inline Local. It can be used if there is an expression in a method that either appears multiple times, or which would make more sense if a name were associated with it. This is sometimes also called Introduce Explaining Variable.
+   - Extract Method - This remarkably convenient refactoring should be used to break up

³Given the rate at which work is being done on Scala and the Eclipse plug-in, it is inevitable that this list will likely be longer for you.