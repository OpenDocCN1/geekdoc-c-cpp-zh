know their ancestor well) can be trusted to use the method correctly, but other classes cannot.

A good example of this kind of method is the clone method of the Object class—see Chapter 6 for more details.

> **C++ NOTE:** As already mentioned, protected features in Java are accessible to all subclasses as well as to all other classes in the same package. This is slightly different from the C++ meaning of protected, and it makes the notion of protected in Java even less safe than in C++.

Here is a summary of the four access control modifiers in Java:

+   1. Accessible in the class only (private).  
+   2. Accessible by the world (public).  
+   3. Accessible in the package and all subclasses (protected).  
+   4. Accessible in the package—the (unfortunate) default. No modifiers are needed.

# 5.2 Object: The Cosmic Superclass

The Object class is the ultimate ancestor—every class in Java extends Object. However, you never have to write

```
public class Employee extends Object
```

The ultimate superclass Object is taken for granted if no superclass is explicitly mentioned. Since every class in Java extends Object, it is important to be familiar with the services provided by the Object class. We go over the basic ones in this chapter; consult the later chapters or view the online documentation for what is not covered here. (Several methods of Object come up only when dealing with concurrency—see Chapter 12.)

# 5.2.1 Variables of Type Object

You can use a variable of type Object to refer to objects of any type:

```
Object obj = new Employee("Harry Hacker", 35000);
```

Of course, a variable of type Object is only useful as a generic holder for arbitrary values. To do anything specific with the value, you need to have some knowledge about the original type and apply a cast: