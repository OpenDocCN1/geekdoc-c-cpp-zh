
### Listing 3.11: “Private” methods in Objective-C

```
@interface Foo : NSObject
{
}

+(id)fooWithArray:(NSMutableArray *)inArray;
-(void)someOtherMethod;

@end

@implementation Foo

+(id)fooWithArray:(NSMutableArray *)inArray
{
    return [[[self alloc] initWithArray:inArray] autorelease];
}

-(void)somePrivateMethod;
{
    // do something private...
}

-(void)someOtherMethod;
{
    [self somePrivateMethod]; // this is OK.
    [self anotherPrivateMethod]; // this generates a warning
}

-(void)anotherPrivateMethod;
{
    // do something else private
}

@end
```

Notice that the first private method is physically above the method that calls it in the file and in the listing. The second private method is below the method that calls it. If you were to do this in your code, the second private method generates a compiler warning just like if you were calling a private method in another class.

> **NOTE:** If this method of declaring “private” methods seems a bit sketchy to you because of the dependency on the location of the definition of the methods in the file, see Chapter 8 for another way of declaring private methods using categories.

## Working with Properties

A recent addition to Objective-C is the concept of properties. Properties allow you to declaratively define accessor methods for the data members of your classes. They eliminate much of the boilerplate code that has been previously required for accessing those data members. They also enable you, the developer of a class, to define the contract for the state of your object. They are an important syntactical addition to Objective-C.

### Understanding the differences between state and behavior

In previous sections, I talked about objects as a mechanism for encapsulating attributes and behavior. In this section, I approach this topic in a bit more depth in order to explain some concepts that can help you in your use of properties in Objective-C.

The purpose of properties in Objective-C is to assist you in exposing attributes of your object that represent your object’s state. Internally, properties compile down to actual methods that can be used to get and set the data in your objects. These are called accessors. You can choose to use the compiler-generated accessors, or you can choose to override the compiler and generate your own.

> **NOTE:** An accessor is a method which is defined specifically for the purpose of allowing users of your objects to set and get values in your object. They encapsulate the data members of your object and hide the implementation details of those objects from the outside. An accessor can allow direct access to a variable, or it can be nothing more than a calculation that is performed when accessed. Sometimes these methods are called setters and getters. Most people use properties instead of manually writing accessors, but in cases where you want to override the normal behavior of property accessors, you can easily override accessors and provide your own implementation. I show you how to do this shortly in the section on properties.

Objects are composed of state and behavior. State consists of the data that makes up your object. When thinking about object state, a good design rule that most developers follow states that though an object’s state can be changed at any time, it is safe to consider that once an object’s state has been set, it will maintain that state until otherwise acted upon by your application. It is also considered to be bad form to have side effects occur when simply modifying the state of an object. When you are tempted to have the act of changing the state of an object have an outside side effect, you should think carefully about the design decisions that have led you to that result.

Behavior, on the other hand, can be thought of as your object taking action. Behavior can be used to update other objects, and thus have side effects, or it can be used to change the internal data of your object or trigger other operations on your object.

Some schools of object-oriented design state that objects should only expose behavior to external entities. With the Objective-C 2.0 property notation, the designers of Objective-C decided that it is acceptable to expose the internal state of your objects as well. The property notation enables you to expose your object’s state while still providing accessors through which the access to that state goes. Properties, similarly, should be used only for accessing and manipulating your object’s state. To be clear, when writing properties, you should not create properties that have far-ranging external consequences. This is the kind of thing that should be limited to behaviors on your objects.

To give you an example, consider a class that represents an engine. This engine class might expose a property for specifying its throttle. Your property to specify the throttle setting should only set the throttle value. If you want to additionally expose behavior that causes the engine to change its behavior based on the throttle value, then you should additionally expose a method (a behavior) called something like updateEngineSpeedFromThrottle. This method would take no parameters, and it would return a Boolean value indicating whether or not it was able to successfully update the engine’s speed based off of the throttle value.

By separating the state and behavior of your class, you are preventing potential side effects and dependencies between your behaviors and your object attributes.

### Using properties to declare object state

For the purposes of this example, I’d like you to imagine that you’re writing an HR application. This application will be used to track employee benefits, including salary, insurance, and so on. Therefore, you need to create an Employee class that will be used to encapsulate this data.

I’m sure that you can imagine the kinds of attributes and properties that an employee class would have to encapsulate. Typically, these would include things like the employee’s first name, their last name, their Social Security number, their employee number, their salary, and perhaps a reference to another employee who is their manager. All these items can be represented as properties of the employee class.

Listing 3.12 shows an example of how you might create the employee class interface. It includes the listing of the data members that I just specified as well as properties for accessing each of those data members. As we explore each of these properties, it should help you to understand how properties work and which attributes properties can have.

### Listing 3.12: The employee class interface

```
#import <Cocoa/Cocoa.h>

@interface Employee : NSObject
{
    NSString *firstName;
    NSString *lastName;
    NSDate *birthDate;
    NSDate *dateOfEmployment;
    Employee *manager;
    NSString *ssn;

    double salary;
}
@property (nonatomic, retain) NSString * firstName;
@property (nonatomic, retain) NSString * lastName;
@property (nonatomic, retain) NSDate * birthDate;
@property (nonatomic, retain) NSDate * dateOfEmployment;
@property (nonatomic, assign) Employee * manager;
@property (nonatomic, retain) NSString * ssn;
@property (nonatomic, readonly) NSTimeInterval age;
@property (nonatomic) double salary;

-(id)initWithFirstName:(NSString *)inFirstName lastName:(NSString *)inLastName birthDate:(NSDate *)inBirthDate ssn:(NSString *)inSsn;
-(id)init;
-(void)giveRaise:(double)percentage;
-(double)bonus;

@end
```

The first thing to note is that almost all the properties specified here have data members that they map to. A property declaration consists of the @property directive followed by attributes that affect the type of accessor that is created as part of this property. These attributes are specified inside the parentheses after the @property directive. The different attributes that can be specified for a given property are shown in Table 3.1.

### Table 3.1: Property Attributes

| Attribute | Purpose |
|---|---|
| getter=&lt;name&gt;, setter=&lt;name&gt; | Specifies the name of the accessor methods that will be used for this property. |
| readwrite or readonly | Specifies whether this property will be able to be written to. Default is readwrite. |
| assign, retain, or copy | Determines the type of setter generated for this property. Assign generates a setter with a plain assign to the variable. Retain generates a setter which retains the argument passed to it while assigning it to the variable. Copy generates an accessor which copies the passed in value to the member variable. The default is assign. |
| nonatomic | Specifies that the generated accessor will be nonatomic, and therefore not threadsafe. The default value is atomic, or threadsafe. |

Following the property attributes, you must specify the datatype for the property. Properties do not always have to map directly to a data member variable, but when they do, that data member’s datatype should match the data type of the property specified here. Finally, you have to specify the name of the property. It is possible to specify a property with a name that is different from the actual data member that the property represents. Most often, however, you won’t need to do this. Therefore, this name should match the name of the data member that this property maps to.

As usual, things declared in your interface file also have a corresponding declaration in your implementation file. Properties are no different. To use the compiler-generated accessor methods, your properties must have a declaration inside of your implementation block in your implementation file. The possible types of property declarations in your implementation file can be either @synthesize declarations or @dynamic declarations. The @synthesize directive causes the compiler to completely generate all the necessary code to create the accessors for your property. Essentially, this directive is a “hands-off” method for using properties. If you use the @synthesize directive, no additional code needs to be written in your implementation file for your property.

On the other hand, if you want to create your accessors yourself, by hand, either in your code or later, by dynamically loading code at runtime, you can do this by using the @dynamic directive. When using the @dynamic directive, the compiler will expect that you have created an appropriate pair of accessors for your property.

> **CAUTION:** When you create your own accessors using the @dynamic directive, ensure that your accessors fulfill the contract that you have specified in the property’s attributes. In other words, if you have specified a copy attribute, then you have to ensure that your accessor copies the value that’s passed in when setting the property.

Listing 3.13 shows our employee class implementation. Note that there are different properties that are handled in different ways.
