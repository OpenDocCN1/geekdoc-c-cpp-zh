The method implementation specifies the instructions required for the computer to execute whatever behavior it is that you want to occur when this method is called. To return a value from a method, you use the return statement just like you did previously when defining procedures.

All the data members of your class are within scope and available to be used within any object method defined for that class. Additionally, any variables passed into the method as arguments are also within scope and available within the method as well.

# Working with the special object methods

In addition to object methods that define behavior that you require for your functionality, there are also certain special object methods that you can optionally define as part of your class that have specific functionality and standard behavior. A variety of these methods exist, but I want to introduce you to two of them right now.

The first of these special object methods are in the generic category of initializers. Initializer method names always begin with the word init and always return an id datatype. Other than these conventions, the method signature of initializers is reasonably arbitrary. However, the body of an initializer method should follow a special standardized syntax. Listing 3.5 shows an example of a typical initializer.

Listing 3.5

# A typical initializer

```
-(id)init
{
    if((self = [super init]))
    {
        memberVariable = [[NSMutableArray alloc] init];
    }
    return self;
}
```

The structure of the initializer method is very important. The first step is to call the superclass designated initializer. The initializer returns an initialized instance of the superclass object, and you must assign that to the special variable "self". If something fails during the initialization process, the contract associated with the initializer specifies that it should return a nil object instead of a validly initialized object. Because of this, after assigning the return of the super class initializer to self, you should check to see if self is nil. If it is, you should not initialize your own variables, but instead, simply return nil yourself. In the example shown above, we actually assign the variable to self and check it for nil at the same time in the if statement.