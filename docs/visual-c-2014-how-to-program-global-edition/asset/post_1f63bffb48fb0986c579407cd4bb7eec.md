
objects and variables. Although a derived-class object also is a base-class object, the two are nevertheless discussed. As discussed previously, derived-class objects can be treated as if they were base-class objects. However, the derived class can have additional derived-class members. For this reason, assigning a base-class reference to a derived-class variable is not allowed without an explicit cast—such as an assignment would leave the derived-class undefined for a base-class object.

We've discussed four ways to assign base-class and derived-class references to base-class and derived-class types:

- 1. Assigning a base-class reference to a base-class variable is straightforward.
- 2. Assigning a derived-class reference to a derived-class variable is straightforward.
- 3. Assigning a derived-class reference to a base-class variable is safe, because the derived-class object is an object of its base class. However, this reference can be used to refer only to base-class members through the base-class variable, the compiler reports errors.
- 4. Attempting to assign a base-class reference to a derived-class variable is a compilation error. To avoid this, the base-class reference must be cast to a derived-class type explicitly or be converted using the operator. At execution time, if the object to which the reference is not a derived-class object, an exception will occur (when you use the operator, in which case you will have to check the expression's result for null). The operator can be used to ensure that such a cast is performed only if the object is a derived-class object.

## 12.6 sealed Methods and Classes

Only methods declared virtual, override or abstract can be overridden in derived classes. A method declared sealed in a base class cannot be overridden in a derived class. Methods that are declared private are implicitly sealed, because it is impossible to override them in a derived class (though the derived class can declare a new method with the same signature as the base class). Methods that are declared static are implicitly sealed, because static methods cannot be overridden. A derived-class method declared sealed can override a sealed base-class method, but cannot be overridden in derived classes further down the inheritance hierarchy.

A sealed method's declaration never changes, so all derived classes use the same method implementation, and calls to sealed methods (and non-virtual methods) are resolved at compile time—this is known as static binding. Since the compiler knows that sealed methods cannot be overridden, it can optimize code by removing sealed methods and replacing them with the sealed code of their declarations at method-call location—a technique called inlining the code.

> The compiler can inline a sealed method call and will do so for small, sealed methods. Inlining does not violate encapsulation or information binding, but does improve performance, it eliminates the overhead of making a method call.

A class that is sealed cannot be a base class (i.e., a class cannot extend a sealed class). All methods in a sealed class are implicitly sealed. Class string is a sealed class. This class cannot be extended, so apps that use strings rely on the functionality of string objects as defined in the Framework Class Library.

> Common Programming Error 12.4
Attempting to declare a member of a sealed class is a compilation error.

## 12.7 Case Study: Creating and Using Interfaces

Our next example (Figs. 12.11–12.14) reexamines the payroll system of Section 12.5. Suppose the company wishes to perform several accounting operations in a single accounts-payable app—in addition to calculating the payroll earnings that must be paid to each employee, the company must also calculate the payment due on several invoices (i.e., bills for goods purchased). Though applied to unrelated things (i.e., employees and invoices), both operations have to do with calculating payment amount. For an invoice, the payment refers to the total cost of the goods listed on the invoice. We can calculate different things as the payments for employees and invoices polymorphically in a single app? Is there a capability that can relate classes to implement a set of common methods (e.g., a method that calculates a payment amount)? Interfaces offer exactly this capability.

### Standardized Interactions
Interfaces define and standardize the ways in which people and systems can interact with one another. For example, the controls on a radio serve as an interface between a radio's users and its internal components. The controls allow users to perform a limited set of operations (e.g., changing the station, adjusting the volume, choosing between AM and FM), and different radios may implement the controls in different ways (e.g., using buttons, dials, voice commands). The interface specifies what operations a radio must permit users to perform but not how they're performed. Similarly, the interface between a driver and a car with a manual transmission includes the steering wheel, the gear shift, the clutch pedal, the gas pedal and the brake pedal. This same interface is found in nearly all manual-transmission cars, enabling anyone who knows how to drive one particular manual car to drive any other. The components of each car may look a bit different, but the general purpose is the same—allow people to drive the car.

### Interfaces in Software
Software objects communicate via interfaces. A C# interface defines a set of methods and properties that can be called on an object—to tell it, to perform some task or return some piece of information. The next example introduces an interface IPayable that describes the functionality of any object that must be capable of being paid and must offer a method to determine the proper payment due. An interface declaration begins with the keyword interface and can contain only

- abstract methods

All interface members are *implicitly* declared public and abstract. In addition, each interface can extend one or more interfaces to create a more elaborate interface that other classes can implement.

> Common Programming Error 12.5
> It's a compilation error to explicitly declare an interface member public or abstract, because they're redundant in interface-member declarations. It's also a compilation error to specify in an interface implementation details, such as concrete method declarations.

### Implementing an Interface

A class must specify that it implements the interface by listing the interface name after the colon ( in the class declaration. This is the same syntax used to indicate inheritance from a base class. A concrete class implementing the interface must declare each member of the interface with the signature specified in the declaration. A class that implements an interface but does not implement all its members is an abstract class—it must be declared abstract and must contain an abstract declaration for each unimplemented member of the interface. Implementing an interface is like signing a contract with the compiler that, "I will provide an implementation for the members specified by the interface, or I will declare them abstract."

> Common Programming Error 12.6
> Failure to define or declare any member of an interface in a class that implements the interface results in a compilation error.

### Common Methods for Unrelated Classes
An interface is typically used when unrelated classes need to *share* common methods. This allows unrelated objects to be processed polymorphically—objects of classes that implement the same interface can respond to the *same method* calls. You can create an interface that describes the desired functionality, then implement this interface in any classes requiring functionality. For example, in the accounts-payable app developed in this section, we implement IPayable in each class (e.g., *Employee*, *Invoice*) that must be able to calculate a payment amount.

### Interfaces vs. Abstract Classes
An interface is often used in place of an abstract class when there's no default implementations to inherit—that is, there are no fields and no default method implementations. Abstract classes are typically public types, so they're normally declared in files by themselves with the same name as the interface and the .cs filename extension.

### 12.7.1 Developing an IPayable Hierarchy

To build an app that can determine payments for employees and invoices alike, we first create an interface IPayable. Interface IPayable contains decimal amount to be paid for an object of any class that implements the methods. Method GetPaymentAmount is a general-purpose method of Earnings of the Employee hierarchy—method Earnings calculates a payment amount specifically for an Employee, while GetPaymentAmount can be applied to a broad range of unrelated objects. After declaring interface IPayable, we introduce class Invoice,
