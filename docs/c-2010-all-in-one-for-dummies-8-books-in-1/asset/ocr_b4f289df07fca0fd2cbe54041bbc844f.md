# How C# Supports Object-Oriented Concepts 213

These C# features are necessary for writing object-oriented programs:

+   * **Controlled access:** C# controls the way in which class members can be accessed C# keywords enable you to declare some members open to the public whereas internal members are protected from view and some secrets are kept private.Notice the little hints. Access controls are revealed in Chapter 5 of this minibook.

+   * **Specialization:** C# supports specialization through a mechanism known as inheritance. One class inherits the members of another class. For example, you can create a Car class as a particular type of Vehicle. C# specializes in specialization.

+   * **Polymorphism:** This feature enables an to perform an operation it wants to. The Rocket type of Vehicle may implement the Start operation much differently from the Car type of Vehicle does. At least, I hope it does every time I turn the key in my car. (With my car, you may not know) But all Vehicles have a Start operation, and you can rely on that Chapter 7 in this minibook finds its own way of describing polymorphism.

+   * **Indirection:** Objects frequently use the services of other objects — by calling their public methods. But classes can "know too much" about the classes they use. The two classes are then said to be "too coupled," which makes the using class too dependent on the used class. The design is too brittle — liable to break if you make changes. But change is inevitable in software, so you should find more indirect ways to connect the two classes. That's where the C# interface comes in. (You can get the scoop on interfaces in Chapter 8 of this minibook.)