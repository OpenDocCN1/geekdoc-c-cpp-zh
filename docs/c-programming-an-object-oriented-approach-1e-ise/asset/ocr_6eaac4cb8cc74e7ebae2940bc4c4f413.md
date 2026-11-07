# ## 11.3 DEPENDENCY

The third type of relationship that we can define between two classes is dependency. Dependency is a weaker relationship than inheritance or association. Although there are several definitions for dependency, we use the one that is most prevalent. We say that dependency models the “uses” relationship. Class A depends on class B if class A somehow uses class B. In other words, class A depends on class B if A cannot perform its complete task without knowing that class B exists. This happens when

+   - Class A uses an object of type B as a parameter in a member function.
+   - Class A has a member function that returns an object of type B.
+   - Class A has a member function that has a local variable of type B.

# ### 11.3.1 UML Diagrams

We use both UML class diagrams and UML sequence diagrams to show dependencies (see Appendix Q).

# ### UML Class Diagram

Although there are many variations of the UML class diagram for dependency, we use the one that shows the dependency with a dashed line and arrow from the depending class to the depended class. Figure 11.21 shows an example of a dependency relationship in which class A depends on class B.

# ### UML Sequence Diagram

A sequence diagram shows the interaction between objects. The main function and each object have lifelines that show the passing of time. The objects can be instantiated and their member function can be called.

As a simple example, we have two classes, First and Second. Class First has a member function called fun() that the user cannot call directly in the application (for some reason such as security). We want to use another function in the Second class called funny() to call the function fun() in the First class. However, we must pass an instance of the First class inside funny() so the First class can use it when it calls its fun() function (Figure 11.22).

In Figure 11.22 the main function instantiates an object of the class First and an object of the class Second. The main function calls the funny(…) member function of the class Second and passes an object of the class First as a parameter. An object of the class Second can then call the fun() function of the class First using the name of the object that received from main. Note that the relationship between objects First and Second is dependency. Object Second uses class First in its member function funny(…), and object Second calls the member function of object First.

# ### 11.3.2 A Comprehensive Example

We use a comprehensive example to demonstrate the basics of dependency relationships. Assume we want to create an invoice for the list of products sold. We have a class named Invoice and a class named Product. The class Invoice uses instances of the class Product as a parameter in one of its member functions (add). Figure 11.23 shows the UML class diagram.

![](bbox=[0.325, 0.812, 0.735, 0.92])