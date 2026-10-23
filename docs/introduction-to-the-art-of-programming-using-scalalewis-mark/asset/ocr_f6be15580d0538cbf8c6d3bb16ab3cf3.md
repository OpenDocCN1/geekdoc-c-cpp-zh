+   - Members and methods that should not be overridden can be declared `final`. You can also make whole `classes` `final` to prevent any other `classes` from extending them.

+   - Scala allows methods/functions, `classes`, and `traits` to type type parameters. These are passed in square brackets that come before any normal parameters in parentheses. This ability leads to parametric polymorphism, another form of universal polymorphism.

+   - When a `class` takes a type parameter, the type must be specified at the point of instantiation with `new`. This is in contrast to parametric functions/methods which can typically infer the proper types of parameters.

+   - You can place bounds on type parameters. Without bounds, the type parameters must be broadly assumed to be of the type `Any`.

# 19.5.2 Exercises

+   1. The code for the properties panels in the `Drawable` subtypes did not do a good job of handling exceptions if the user typed in something that was not a number. Edit the code to fix this.

+   2. The `DrawRectangle` and `DrawEllipse` classes shared a significant amount of code. Indeed, the two files only differed in that “Rectangle” was replaced by “Ellipse” in a few locations. Edit the code so that you have a single class called `DrawBoundedShape` that keeps the same member data as these classes, but abstracts over the exact shape that is created. There are several ways of doing this. One uses a function of `(Double,Double) => Shape`.

+   3. The `hourFromTime` method in the `ToDValues` class is not particularly robust. What are some situations where it could fail? Write a better replacement for it.

4. Draw out the inheritance hierarchies that you might design to represent the following types of objects.

+   - Animal Life
+   - School/University organization
+   - Accounts for a large bank (savings, checking, etc.)
+   - Types of Facebook friends
+   - Types of students at your school
+   - Whatever else you can think of that makes a good example of an “is-a” relationship.

+   5. Implement one of your hierarchies from above with a few simple methods.

# 19.5.3 Projects

There are several different options here that you could pick from based on which of the projects you started in the last chapter. The general idea though is that you will build a hierarchy of types for things that are related to your project. You can also put in parametric polymorphism if it fits your project.