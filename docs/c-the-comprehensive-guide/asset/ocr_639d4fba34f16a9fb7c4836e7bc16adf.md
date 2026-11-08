# Chapter 19

# Good Code, 5th Dan: Classical Object-Oriented Design

+   ### Chapter Telegram
+   
+   - **Object-oriented programming (OOP)**  
+     Object-oriented programming.
+   - **SOLID**  
+     Acronym for five important OOP principles that help in the design of large projects.
+   - **Single responsibility principle (SRP)**  
+     A class should have only one reason to change.
+   - **Open/closed principle (OCP)**  
+     Classes, functions, and modules should be *open* for extensions but *closed* for modifications.
+   - **Liskov substitution principle (LSP)**  
+     Instances of a derived type should be able to replace instances of the base type.
+   - **Interface segregation principle (ISP)**  
+     No client should be forced to depend on methods it does not use.
+   - **Dependency inversion principle**  
+     Modules should depend on abstractions, not on other modules.
+   - **Covariance**  
+     Return types can be more specific than those of the supertype.
+   - **Contravariance**  
+     Arguments can be more general than those of the supertype.
+   - **Model-view-controller (MVC)**  
+     MVC is a popular architectural pattern.

In *Chapter 15*, you have seen how to derive classes from each other in C++ using *inheritance*. In very brief terms, I also explained some central concepts of *object-oriented programming* there, particularly the difference between the *has-a* relationship and the *is-a* relationship.

However, there is more to OOP:

+   - **Abstraction**  
+     You find commonalities between your objects, defining their methods and functions as generally and generically as possible.