# 4. Terminated

Your app is no longer running.

# 3.1.3 A Note about Frameworks

The great thing about frameworks is that they enable your app to take advantage of ready-made behaviour. Because bada’s language is C++, bada’s frameworks use C++ inheritance to share behaviour between the frameworks and your app. If you know your C++, you’ll probably know (at least approximately) how that works, but it doesn’t matter if you don’t. The principle is simple: the frameworks declare certain methods that your app must implement; the frameworks will call these methods, and when they do, your implementations will run.

The bada C++ frameworks use derivation and virtual functions to share responsibilities between the framework itself, and apps that use the frameworks. The framework base classes that apps derive from provide ready-made implementations of common behaviour that all apps will share, as well as behaviour defined in virtual methods that may optionally be overridden, and abstract behaviour defined in pure virtual methods for which the derived class must provide an implementation. Abstract classes are used extensively in bada, particularly to define interface classes. See Chapter 4 for more about interface classes and how to use them.

> Note: In C++, derivation (i.e. inheritance) is the generic mechanism that allows derived classes to share the behaviour of base classes; and specifically, virtual functions (dynamic binding) allow derived classes to extend the behaviour of base classes by overriding the base class behaviour. Overriding is not the same as overloading, in which methods with the same name but different signatures are allowed, and the references are resolved at compile time; virtual methods use the virtual keyword and have the same name and signature, and the references are resolved at runtime.
> 
> In C++, pure virtual methods, also known as abstract methods, are declared with a special =0; syntax that indicates the method has a null body, that is, no implementation; code won’t link until an implementation is provided.
> 
> Pure virtual methods in the base class must be implemented by a derived class;¹ other virtual methods of the base class have a base class implementation, but optionally may be reimplemented by a derived class to override the default behaviour.

¹More precisely, a derived class that will be instantiated must implement the pure virtuals of its base class(es). Chains of abstract classes are possible, but a class that does not implement an inherited pure virtual is itself an abstract class that cannot be instantiated.