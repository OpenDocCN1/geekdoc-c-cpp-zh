# 6 Glossary of Terms

# Abstract

Something which is abstract does not have a "proper" existence as such. When writing programs we use the word to mean "an idealised description of something". In the case of component design an abstract class contains descriptions of things which need to be present, but it does not say how they are to be realised. In C# terms a class is abstract if it is marked as such, or if it contains one or more method which is marked as abstract.

You can't make an instance of an abstract class, but you can use it as the basis of, or template for, a concrete one. For example, we may decide that we need many different kinds of receipt in our transaction processing system: cash receipt, cheque receipt, wholesaler receipt etc. We don't know how each particular receipt will work inside, but we do know those behaviours which it must have to make it into a receipt.

We can therefore create an abstract Receipt class which serves as the basis of all the concrete ones. Each "real" receipt class is created by extending the parent, abstract one. This means that it is a member of the receipt family (i.e. it can be treated as a Receipt) but it works in its own way.

# Accessor

An accessor is a method which provides access to the value managed within a class. Effectively the access is read only, in that the data is held securely in the class but code in other classes may need to have access to the value itself. An accessor is implemented as a public method which will return a value to the caller. Note that if the thing being given access to is managed by reference the programmer must make sure that it is OK for a reference to the object is passed out. If the object is not to be changed it may be necessary to make a copy of the object to return to the caller.

# Base

base is a C# keyword which has different meanings depending on the context in which it is given. It is used in a constructor of a child class to call the constructor in the parent. It is also used in overriding methods to call the method which they have overridden.

# Call

When you want to use a method, you call it. When a method is called the sequence of execution switches to that method, starting at the first statement in its body. When the end of the method, or the return statement, is reached the sequence of execution returns to the statement immediately following the method call.

# Class

A class is a collection of behaviours (methods) and data (properties). It can be used to represent a real world item in your program (for example bank account). Whenever you need to collect a number of things into a single unit you should think in terms of creating a class.