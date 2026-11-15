# SUMMARY

This chapter discussed how to specialize a class by deriving from it and adding additional methods and properties. This included a discussion of the private and protected access modifiers that control the level of encapsulation.

This chapter also investigated the details of overriding the base class implementation, and alternatively hiding it using the new modifier. To control overriding, C# provides the virtual modifier, which identifies to the deriving class developer which members she intends for derivation. For preventing any derivation altogether you learned about the sealed modifier on the class. Similarly, the sealed modifier on a member prevents further overriding from subclasses.

This chapter ended with a brief discussion of how all types derive from object. Chapter 9 discusses this derivation further, with a look at how object includes three virtual methods with specific rules and guidelines that govern overloading. Before you get there, however, you need to consider another programming paradigm that builds on object-oriented programming: interfaces. This is the subject of Chapter 7.