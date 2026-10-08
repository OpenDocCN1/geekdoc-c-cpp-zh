# 338 Using an Interface

common other than implementing the interface. They don't even have to come from the same class hierarchy, which truly simplifies the designing of hierarchies, for example.

Overworked word: Programmers use the term interface in more than one way. You can see the C# keyword interface and how it's used. People also talk about a class's public interface, or the public methods and properties that it exposes to the outside world. I keep the distinction clear by saying C# interface most of the time when that's what I mean, and saying public interface when I refer to a class's set of methods.

![](bbox=[0.135, 0.198, 0.233, 0.355])

C# structures can implement interfaces just as classes can.

# Using an Interface

In addition to your being able to use a C# interface for a parameter type, an interface is useful as

+   * A method return type
* The base type of a highly general array or collection
* A more general kind of object reference for variable types

I explain the advantage of using a C# interface as a method parameter type in the previous section. Now I tell you about other interfaces.

# As a method return type

I like to form out to a factory method the task of creating the key objects I need. Suppose that I have a variable like this:

```
IRecordable recorder = null; // Yes, you can have interface-type variables.
```

Somewhere, maybe in my constructor, I call a factory method to deliver a particular kind of Iecordable object:

```
recorder = MyClass.CreateRecorder('Pen'); // A factory method is static.
```

where CreateRecorder () is a method, often on the same class, that returns not reference to a Pen but, rather, an Iecordable reference:

```
static Iecordable CreateRecorder(string recorderType)
{
if(recorderType == "Pen") return new Pen();
}
```

I say more about the factory idea later in this chapter. But note that the return type for CreateRecorder () is an interface type.