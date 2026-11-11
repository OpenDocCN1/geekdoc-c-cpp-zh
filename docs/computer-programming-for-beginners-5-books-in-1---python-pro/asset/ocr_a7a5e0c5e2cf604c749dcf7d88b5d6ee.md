each other. Let’s take a module as an example. We can have two different modules that define a function with the same name, however they will not be confused with each other. They are unique and independent.

Python creates namespaces as soon as you run the interpreter, however some of them are enabled at different times and last for certain periods of time. For instance the namespaces that are built into Python will never be deleted. Furthermore, when a module is read in, a global namespace is defined for it, however when we close the interpreter it will be gone.

Keep in mind that while certain namespaces are pre-defined, we don’t necessarily have the ability to access them from anywhere. This is when scope comes into play once again. In this case, scope also represents the section of the application from which we have access to a namespace directly. While in the previous chapter we discussed global and local scopes, here we have three of them generally speaking. The first scope is that of a function and it has a local namespace. The second is the module which creates a global namespace. Finally, we have the third one, which is the general scope that contains all the pre-built, default namespaces.

# **Defining a Class**

Let's start with the class syntax. Here is an example of the most basic kind of class:

```
    class Raven:

        <myStatement1>

        <myStatement2>

        <myStatementN>
```

In a way, defining a class works nearly the same as defining a function. The class definitions are executed before we see the actual effect. However, keep in mind that the statements inside the definition will often be in the form of function definitions.

Regarding the syntax, as you can see we need to use the keyword “class” followed by the name of that class. In addition, you may have noticed that the name starts with a capitalized letter. The naming standard for classes doesn't not follow the same rules as the naming conventions for variables and functions. Keep