
Tragically, if you don't realize what a function pointer is and how to use delegates, then you will write code that is equivalent to two-legged stools.

Event declarations are straightforward. Generally, events are likely to be used by class consumers, so they are commonly declared as public members. A syntax example is shown below.

The access modifier is commonly `public`. The `event` keyword indicates that this member is an event. The delegate type is a class that is described by a method signature and uses the keyword `delegate`. An example of an existing delegate is the `EventHandler` delegate. The event name is the member name of the event; this is what consumers will use to refer to the event in code. The following statement declares an event using the `EventHandler` delegate.

The signature of `EventHandler` is a method that returns `void` and has two parameters, `object` and `System.EventArgs`. The declaration of the `EventHandler` delegate exists in the CLR as

(This delegate already exists; accordingly, you don't need to define it yourself.)

`EventHandler` is the delegate used for many Windows Forms controls, similar to the `Button` control's `Click` event.

## Declaring New Delegate Types

If you need to define a custom delegate, you can follow the basic model given in the previous section demonstrating the `EventHandler` delegate.

A delegate definition is actually equivalent to a method header with the keyword `delegate` included between the access modifier and the return type. The following example defines another delegate for a method that returns `void` and takes no arguments.

```
public delegate void Delegate();
```

Review that C# is case-sensitive and note that the first example presents a delegate named "Delegate." Any method that returns `void` and takes no arguments can be assigned to events or fields that are declared as `Delegate` types.

### Raising Events as a Producer

Producers raise events. Raising an event in C# is performed by calling a method using the event name. By convention, events are raised by protected members with a similar name as the event with "On" as a prefix.

Coming back to our unique case of the `Changed` event defined as an `EventHandler` type, we can match the event with a protected method that raises the event.

The event is named `Changed`. Consumers can assign any number of methods that match the signature of the `EventHandler` delegate to this one event member. Inside the class containing the code, you would call `OnChanged` anywhere that you need to raise the `Changed` event. `OnChanged` checks to ensure that `Changed` has been assigned to at least one delegate; if it hasn't, then `OnChanged` returns. Otherwise, `Changed` is treated like a method by the producer and is called, with the producer passing it the vital arguments.

When a producer raises an event with a `sender` parameter, that value is constantly set to the internal reference to self: `this`. In our basic model, we pass a null `System.EventArgs` parameter since we are not using that value. If you have to pass specific values to a consumer's event handler, then you can make an instance of `System.EventArgs` or make a delegate that takes a particular subclass of `EventArgs`.

### Handling Events as a Consumer

Consumers handle events by wiring an event handler to an event member of an object. The model program `EventsDemo.sln` contains the classes `EventChanged` and `Form1`. For our situation, we expect that `Form1` contains an `EventChanged` object and needs to handle the `EventChanged.Changed` event. For this to work `Form1` needs to make an instance of `EventChanged` and assign a method to `EventChanged.Changed`.

The following model exhibits code in `Form1` that wires an event handler to `EventChanged`.

The `EventChanged` object is named `obj` and launched as a field in the form. `Form1_Load` (an event itself) wires the `EventChanged.Changed` event to `Form1`'s `button1_Click` method. (The button click method was already accessible and happens to have a similar signature as the `Changed` event.) The `+=` operator is used to assign the new `System.EventHandler` object to `Changed`. Doing this will add the event handler to the invocation list.

Just the `+=` and `-=` operators are overloaded to attach and remove event handlers from an event's invocation list. You can't use the assignment operator to assign a delegate to an event.

Think of an event declaration as a field whose type is a delegate type: a delegate. When you assign a delegate to the event, you are inserting the delegate into a list that is a member of the delegate type. When you raise the event by invoking the event as a method call, you are really invoking the delegate.

When the event method is called internally, it iterates through all of the delegates attached to the internal list and calls every single one of them.

Coming back to our model containing the public event `EventHandler Changed`, when we raise the event by calling `Changed`, each delegate assigned to `Changed` is called. This is referred to as multicasting. Delegates can be bound to a single method or to multiple methods.

It is conceivable to layer a few bits of functionality into one event by assigning several delegates to a single event. What you ought not do is depend on delegates being called in a particular order.

## Creating Programs

Invoking the constructor using the `new` operator. You can make instances of objects and assign them to variables whose type is the same type as the object instantiated or a type in the object's inheritance. That is, instances of child types can be assigned to variables declared as a kind of the object's parent. The reverse isn't valid. (See the upcoming section "Inheritance" for more data.) Remember that constructors have a similar name as the class, can have public or non-public modifiers, and may have at least zero parameters. Constructors can be overloaded. Along these lines, there might be more than one constructor that is appropriate for you to call. Here are a few examples showing object instantiation.

The first statement makes an instance of the `FileStream` class. (You should add the `System.IO` namespace to your application with a `using` directive to use the `FileStream` class.) `FileStream` objects have a few constructors. The model used takes a file path and a `FileMode`. Remember that C# strings use the backslash (`\`) as an escape character; you should use the `\\` backslash pair when you mean backslash inside a string. The subsequent statement shows an inline construction of an array of bytes with an initializer list.

The first array model shows building an array of strings with extra space for 10 strings. Valid indexes for arrays in C# are 0 to n – 1, where n represents the number of elements in the array. The subsequent model develops an array of numbers using an initializer list. The initializer list gives the values to the array and the length. The size of the numbers is 6, and valid indexes are 0 to 5. In C# you can specify both the number of elements and an initializer list for arrays, but you don't need both.

## Defining Interfaces

Interfaces enable you to define a contract for your classes. In the object-oriented world, we have inheritance, composition, and association. Inheritance describes a relationship where another thing is a specialization of a current thing. For instance, a Jeep is a specialization of a vehicle and can be described using inheritance. Jeeps have transmissions, exhibiting an aggregation relationship. A Jeep may likewise have a driver, which is an example of an association relationship. The transmission belongs to the Jeep, yet the driver doesn't.

Interfaces portray connections that can sometimes be defined in different manners, similar to inheritance, aggregation, or association, but may best be described as
