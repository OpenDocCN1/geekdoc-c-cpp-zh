
- Use specially provided datatypes, such as for collections
- Implement a specific interface
- Provide specific constructors
- Provide mandatory specific fields
- Avoid certain constructs

There is at least one more, and one that is so obvious that I forgot. You shouldn't have to write database code such as calls to stored procedures in your Domain Model classes. But that was so obvious that I didn't write specifically about it.

Let's take a closer look at each of the other points.

## Inherit from a Certain Base Class

With frameworks, a very common requirement for supporting persistence is that they require you to inherit from a certain base class provided by the framework.

The following might not look too bad:

```csharp
public class Customer : PersistentObjectBase
{
    public string Name = string.Empty;

    ...

    public decimal CalculateDepth()
    ...
}
```

Well, it wasn't too bad, but it did carry some semantics and mechanisms that aren't optimal for you. For example, you have used the only inheritance possibility you have for your Customer class because .NET only has single inheritance. It's certainly arguable whether this is a big problem or not, though, because you can often design "around" it.

It's a worse problem if you have developed a Domain Model and now you would like to make it persistent. The inheritance requirement might very well require some changes to your Domain Model. It's pretty much the same way you start developing a Domain Model with TDD. You have the restriction from the beginning that you can't use inheritance and have to save that for the persistence requirement.

Something you should look out for is if the inheritance brings lots of public functionality to the subclass, which might make the consumer of the subclass have to wade through methods that aren't interesting to him.

It's also the case that it's not usually as clean as the previous example, but most of the time PersistentObjectBase forces you to provide some method implementations to methods in PersistentObjectBase, as in the Template Method pattern [GoF Design Patterns]. OK, this is still not a disaster, but it all adds up.

### Note

This doesn't necessarily have to be a requirement, but can be seen as a convenience enabling you to get most, if not all, of the interface implementation that is required by the framework if the framework is of that kind of style. We will discuss this common requirement in a later section.

This is how it was done in the Valhalla framework that Christoffer Skjoldborg and I developed. But to be honest, in that case there was so much work that was taken care of by the base class called EntityBase that implementing the interfaces with custom code instead of inheriting from EntityBase was really just a theoretical option.

## Only Instantiate via a Provided Factory

Don't get me wrong, I'm not in any way against using factories. Nevertheless, I'm not ecstatic at being forced to use them when it's not my own sound decision. This means, for instance, that instead of writing code like this:

```csharp
Customer c = new Customer();
```

I have to write code like this:

```csharp
Customer c = (Customer)PersistentObjectFactory.CreateInstance(typeof(Customer));
```

### Note

I know, you think I did my best to be unfair by using extremely long names, but this isn't really any better, is it?

```csharp
Customer c = (Customer)POF.CI(typeof(Customer));
```

Again, it's not a disaster, but it's not optimal in most cases. This code just looks a lot weirder than the first instantiation code, doesn't it? And what often happens is that code like this increases testing complexity.

Often one of the reasons for the mandatory use of a provided factory is that you will consequently get help with dirty checking. So your Domain Model classes will get subclassed dynamically, and in

You could get help with bi-directionality so that you don't have to code it on your own. This is yet another example of something an AOP solution can take care of for you.

## Implement a Specific Interface

Yet another very regular requirement on Domain Model classes for being persistable is that they implement one or more infrastructure-provided interfaces.

This is naturally a smaller problem if there is very little code you have to write in order to implement the interface(s) and a bigger problem if the opposite is true.

One example of interface-based functionality could be to make it possible to fill the instance with values from the database without hitting setters (which might have specific code that you don't want to execute during reconstitution).

Another common example is to provide interfaces for optimized access to the state in the instances.

## Provide Specific Constructors

Yet another way of providing values that reconstitute instances from the database is by requiring specific constructors, which are constructors that have nothing at all to do with the business problem at hand.

It might also be that a default constructor is needed so that the framework can instantiate Domain Model classes easily as the result of a Get operation against the database. Again, it's not a very dramatic problem, but a distraction nonetheless.

## Provide Mandatory Specific Fields

Some infrastructure solutions require your Domain Model classes to provide specific fields, such as Guid-based Id-fields or int-based Version-fields. (With Guid-based Id-fields, I mean that the Id-fields are using Guids as the datatype.) That simplifies the infrastructure, but it might make your life as a Domain Model-developer a bit harder. At least if it affects your classes in a way you didn't want to.

## Avoid Certain Constructs/Forced Usage of Certain Constructs

I have already mentioned that you might be forced to use virtual properties even if you don't really want to. It might also be that you have to avoid certain constructs, and a typical example of this is read-only fields. Read-only (as when the keyword readonly is used) fields can't be set from the outside (except with constructors), something that is needed to create 100% PI-Domain Model classes.

Using a private field together with a get-only property is pretty close to a read-only field, but not

### Note

Mark Burhop commented as follows:

Hmmm... This was the original argument against C++ from C programmers in the early 90s. "C++ sticks in new code I didn't write." "C++ hides what is really going on." I don't know that this argument holds much water anymore.

It's also harder to inject code at the byte level for .NET classes compared to Java. It's not supported by the framework, so you're on your own, which makes it a showstopper in most cases.

What is most often done instead is to use some alternative techniques, such as those I mentioned with runtime-subclassing in combination with a provided factory, but it's not a big difference compared to injected code. Let's summarize with calling it emitting code.

## The Cost for PI Entities/Value Objects

I guess one possible reaction to all this is "PI seems great why not use it all the time?" It's a law of nature (or at least software) that when everything seems neat and clean and great and without fault, then come the drawbacks. In this case, I think one such is overhead.

I did mention earlier in this chapter that speed is something you will sacrifice for a high level of PI-ness, at least for runtime PI, because you are then directed to use reflection, which is quite expensive. (If you think compile-time PI is good enough, you don't need to use reflection, but can go for an AOP solution instead and you can get a better performance story.)

You can easily prove with some operation in a tight loop that it is magnitudes slower for reading from/writing to fields/properties with reflection compared to calling them in the ordinary way. Yet, is the cost too high? It obviously depends on the situation. You'll have to run tests to see how it applies to your own case. Don't forget that a jump to the database is very expensive compared to a lot you're doing in your Domain Model, yet at the same time, you aren't comparing apples and apples here. For instance, the comparison might not be between an ordinary read and a reflection-based read.

### A Typical Example Regarding Speed

Let's take an example to give you a better understanding of the whole thing. One common operation in a persistence framework is deciding whether or not an instance should be stored to the database at the end of a scenario. A common solution to this is to let the instance be responsible for signaling IsDirty if it is to be stored. Or better still, the instance could also signal itself to the Unit of Work when it gets dirty so that the Unit of Work will remember that when it's time to store changes.

But (you know there had to be a "but," right?) that requires some abuse of PI, unless you have paid with AOP.
