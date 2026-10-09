Open Employee.m and synthesize the accessors:

```
#import "Employee.h"
@implementation Employee

@synthesize employeeID;

@end
```

Now you have a new **Employee** class with all the instance variables of **Person** and a new instance variable called employeeID. Instances of **Employee** will respond to all the same messages that an instance of **Person** will. Instances of **Employee** will also respond to the messages setEmployeeID: and employeeID.

And, because **Person** inherits from NSobject, **Employee** also inherits all the instance variables and methods from NSobject. All objects inherit (either directly or indirectly) from NSobject.

NSobject has many methods, but only one instance variable: the isa pointer. Every object’s isa pointer points back to the class that created it.

# Figure 18.2 Object diagram for BMITime

![](bbox=[0.2, 0.43, 0.81, 0.69])

Let’s say that you send the message fido to an object. In order to respond to this message, the object uses the isa pointer to find its class and ask, “Do you have an instance method named fido?” If the class has a method named fido, it gets executed. If the class doesn’t have a fido method, it asks its superclass, “Do you have an instance method called fido?” And up, up the chain it goes on the hunt for a method named fido. The hunt stops when the method is found or when the top of the chain is reached. At the top of the chain, NSobject says, “Nope, no fido method.” Then you get an error message that says something like “This instance of **Employee** does not respond to the fido selector.”