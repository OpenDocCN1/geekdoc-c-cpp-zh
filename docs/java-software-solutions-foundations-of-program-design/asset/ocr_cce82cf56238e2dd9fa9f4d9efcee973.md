# 4.2 Anatomy of a Class

SR 4.5 A class is the blueprint of an object. It defines the variables and methods that will be a part of every object that is instantiated from it. But a class reserves no memory space for variables. Each object has its own data space and, therefore, its own state.

SR 4.6 The instance data of the Die class are MAX, an integer constant equal to 6 that represents the number of faces on the die and therefore the maximum value of the die, and faceValue, an integer variable that represents the current “up” or face value of the die.

SR 4.7 The methods defined for the Die class that can change the state of a Die object are roll and setFaceValue.

SR 4.8 When you pass an object to a print or println method, the toString method of the object is called automatically to obtain a string description of the object. If no toString method is defined for the object, then a default string is used. Therefore, it is usually a good idea to define a toString method when defining classes.

SR 4.9 The scope of a variable is the area within a program in which the variable can be referenced. An instance variable, declared at the class level, can be referenced in any method of the class. Local variables, including the formal parameters, declared within a particular method, can be referenced only in that method.

SR 4.10 A UML diagram helps us visualize the entities (classes and objects) in a program as well as the relationships among them. UML diagrams are tools that help us capture the design of a program prior to writing it.

# 4.3 Encapsulation

SR 4.11 A self-governing object is one that controls the values of its own data. Encapsulated objects, which don’t allow an external client to reach in and change its data, are self-governing.

SR 4.12 An object’s interface is the set of public operations (methods) defined on it. That is, the interface establishes the set of services the object will perform for the rest of the system.

SR 4.13 A modifier is a Java reserved word that can be used in the definition of a variable or method and that specifically defines certain characteristics of its use. For example, by declaring a variable with private visibility, the variable cannot be directly accessed outside of the object in which it is defined.