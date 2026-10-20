
## 3 | Expressing Designs in C#

Beginners using a foreign (human) language can manage to communicate. They know the words, and they can piece them together to get their point across. As beginners transition to experts in a language, they begin to use the proper idioms in this foreign language. The language becomes less foreign, and the person begins speaking more efficiently and more clearly. Programming languages are no different. The techniques you choose communicate your design intent to the developers who maintain, extend, or use the software you develop. C# types all live inside the .NET environment. The environment makes some assumptions about the capabilities of all types as well. If you violate those assumptions, you increase the likelihood that your types won’t function correctly.

The items in this chapter are not a compendium of software design techniques—entire volumes have been written about software design. Instead, these items highlight how different C# language features can best express the intent of your software design. The C# language designers added language features to more clearly express modern design idioms. The distinctions among certain language features are subtle, and you often have many alternatives to choose from. More than one alternative might seem “best” at first; the distinctions show up only later, when you find that you must enhance an existing program. Make sure you understand these items well, and apply them carefully with an eye toward the most likely enhancements to the systems you are building.

Some syntax changes give you new vocabulary to describe the idioms you use every day. Properties, indexers, events, and delegates are examples, as is the difference between classes and interfaces: Classes define types. Interfaces declare behavior. Base classes declare types and define common behavior for a related set of types. Other design idioms have changed because of the Garbage Collector. Still others have changed because most variables are reference types.

The recommendations in this chapter will help you pick the most natural expression for your designs. This will enable you to create software that is easier to maintain, easier to extend, and easier to use.

### Item 21: Limit Visibility of Your Types

Not everybody needs to see everything. Not every type you create needs to be public. You should give each type the least visibility necessary to accomplish your purpose. That’s often less visibility than you think. Internal or private classes can implement public interfaces. All clients can access the functionality defined in the public interfaces declared in a private type.

It’s just too easy to create public types. And, it’s often expedient to do just that. Many standalone classes that you create should be internal. You can further limit visibility by creating protected or private classes nested inside your original class. The less visibility there is, the less the entire system changes when you make updates later. The fewer places that can access a piece of code, the fewer places you must change when you modify it.

Expose only what needs to be exposed. Try implementing public interfaces with less visible classes. You’ll find examples using the Enumerator pattern throughout the .NET Framework library. System.Collections.Generic.List<T> contains a private class, Enumerator<T>, that implements the IEnumerator<T> interface:

```csharp
// For illustration, not complete source
public class List<T> : IEnumerable<T>
{
    private class Enumerator<T> : IEnumerator<T>
    {
        // Contains specific implementation of
        // MoveNext(), Reset(), and Current.
        public Enumerator(List<T> storage)
        {
            // elided
        }
    }

    public IEnumerator<T> GetEnumerator()
    {
        return new Enumerator<T>(this);
    }

    // other List members.
}
```

Client code, written by you, never needs to know about the class Enumerator<T>. All you need to know is that you get an object that implements the IEnumerator<T> interface when you call the GetEnumerator function on a List<T> object. The specific type is an implementation detail. The .NET Framework designers followed this same pattern with the other collection classes: Dictionary<T> contains a private DictionaryEnumerator<T>, Queue<T> contains a QueueEnumerator<T>, and so on. The enumerator class being private gives many advantages. First, the List<T> class can completely replace the type implementing IEnumerator<T>, and you’d be none the wiser. Nothing breaks. Also, the enumerator class need not be Common Language Specification (CLS) compliant. It’s not public (see Item 49). Its public interface is compliant. You can use the enumerator without detailed knowledge about the class that implements it.

Creating internal classes is an often-overlooked method of limiting the scope of types. By default, most programmers create public classes all the time, without any thought to the alternatives. It’s that VS .NET wizard thing. Instead of unthinkingly accepting the default, you should give careful thought to where your new type will be used. Is it useful to all clients, or is it primarily used internally in this one assembly?

Exposing your functionality using interfaces enables you to more easily create internal classes without limiting their usefulness outside the assembly (see Item 26). Does the type need to be public, or is an aggregation of interfaces a better way to describe its functionality? Internal classes allow you to replace the class with a different version, as long as it implements the same interfaces. As an example, consider a class that validates phone numbers:

```csharp
public class PhoneValidator
{
    public bool ValidateNumber(PhoneNumber ph)
    {
        // perform validation.
        // Check for valid area code, exchange.
        return true;
    }
}
```

Months pass, and this class works fine. Then you get a request to handle international phone numbers. The previous PhoneValidator fails. It was coded to handle only U.S. phone numbers. You still need the U.S. Phone Validator, but now you need to use an international version in one installation. Rather than stick the extra functionality in this one class, you’re better off reducing the coupling between the different items. You create an interface to validate any phone number:

```csharp
public interface IPhoneValidator
{
    bool ValidateNumber(PhoneNumber ph);
}
```

Next, change the existing phone validator to implement that interface, and make it an internal class:

```csharp
internal class USPhoneValidator : IPhoneValidator
{
    public bool ValidateNumber(PhoneNumber ph)
    {
        // perform validation.
        // Check for valid area code, exchange.
        return true;
    }
}
```

Finally, you can create a class for international phone validators:

```csharp
internal class InternationalPhoneValidator : IPhoneValidator
{
    public bool ValidateNumber(PhoneNumber ph)
    {
        // perform validation.
        // Check international code.
        // Check specific phone number rules.
        return true;
    }
}
```

To finish this implementation, you need to create the proper class based on the type of the phone number. You can use the factory pattern for this purpose. Outside the assembly, only the interface is visible. The classes, which are specific for different regions in the world, are visible only inside the assembly. You can add different validation classes for different regions without disturbing any other assemblies in the system. By limiting the scope of the classes, you have limited the code you need to change to update and extend the entire system.

You could also create a public abstract base class for PhoneValidator, which could contain common implementation algorithms. The consumers could access the public functionality through the accessible base class. In this example, I prefer the implementation using public interfaces because there is little, if any, shared functionality. Other uses would be better served with public abstract base classes. Either way you implement it, fewer classes are publicly accessible.

In addition, fewer public types will create a smaller public surface area that will facilitate unit testing coverage. If there are fewer public types, there are fewer publicly accessible methods for which you need to create tests. Also, if more of the public APIs are exposed through interfaces, you have automatically created a system whereby you can replace those types using some kind of stubs for unit test purposes.

Those classes and interfaces that you expose publicly to the outside world are your contract: You must live up to them. The more cluttered that interface is, the more constrained your future direction is. The fewer public types you expose, the more options you have to extend and modify any implementation in the future.

### Item 22: Prefer Defining and Implementing Interfaces to Inheritance

