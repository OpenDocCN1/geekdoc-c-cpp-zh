
released through the finally clause underneath. This allows other threads that are waiting on the lock to continue running (well, one at a time of course, due to mutual exclusion), but they will now do so from an inconsistent state. The key message here is this: Avoid throwing during the time a lock is held.

## Summary

Congratulations. After having read this and Chapter 6, “A Primer on Types and Objects,” you’re pretty much an expert in procedural programming techniques now, employing the whole reach of the C# statements spectrum. In this chapter, we discussed different parts of the exception-handling system, most notably focusing on how to write code that’s robust in the face of exceptions but also showing how to throw exceptions ourselves.

Next, we took a look at constructs that build on the exception-handling system, such as proper resource cleanup with the using statement and coordination of concurrent code using mutual exclusion provided by the lock statement.

In the next chapter, we continue to zoom out and look at classes, structs, and containers for them in the form of namespaces. You’ll learn how to create your own types using object-oriented principles and provide typical members for them such as constructors, methods, properties, and indexers.

## CHAPTER 9

### Introducing Types

### IN THIS CHAPTER

- Types Revisited 463
- Classes Versus Structs 466
- Type Members 486

Step by step, we're emerging from the cave of discrete language elements and starting to combine them into large programs. After our extensive coverage of expressions and statements, time has come to use them in a broader context. In this and the following few chapters, we lay the basis for “programming in the large,” exploring classes and structs as well as the various sorts of members they support.

In this chapter, we focus on the concept of types and contrast classes and structs. The discussion of a type's members is deferred until further chapters.

## Types Revisited

At the heart of managed code lies the concept of types. Defining the concept of a type is not an easy task, but put simply, it offers a means for the runtime to know what precisely a certain object is, and hence what the valid operations are to be performed on it. Typing is a crucial concept in the world of managed code because of the type-safety guarantees the platform offers.

Types are blueprints for objects. They describe the shape of objects that are said to have that particular type. Such a shape has two key elements:

- Data is what an object contains and operates on. It directly relates to the layout of objects in memory because storage needs to be provided for all the discrete pieces of data that make up an object.

**Operations** are defined to offer functionality that operates over the data, possibly taking in and/or returning other pieces of data (which by themselves have types).

If you read carefully, you can spot a recursive nature in this definition. While a type defines the shape of an object, it does so by wrapping up pieces of data and providing operations over it. All data involved has a type by itself, too. Obviously, this needs to end somewhere. This is where primitive types enter the picture. For example, some type representing a Person may contain a name stored as a string as well as a date of birth stored as a DateTime. Notice that DateTime by itself can be broken down further into year, month, day, and so on. But ultimately, the DateTime type contains some integral values that describe a date and time unambiguously.

In addition to the code + data breakdown, types can be categorized as concrete versus abstract. Concrete types can have instances of them, whereas abstract ones can't. *Abstract types* provide a means to define proper *type hierarchies*, where parts of a type's implementation are left to extenders of a type. Interfaces are the canonical example of such abstract types, defining a set of operations as a contract for collaboration between different components: "If you implement this and that operation, we're in business."

The simplest way to remember the relationships in which a type participates is to think in terms of verbs. The "is a" relationship denotes a type hierarchy. Every Person is also an Object. To describe the data a type combines together, the "has a" relationship fits it all. And finally, to describe operations, "can" seems an appropriate choice.

Figure 9.1 contains more information than we've characterized so far. It states that Person and Object are classes, denoting the sort of type we're dealing with. After we've expanded a type definition, collapsible regions appear for the different kinds of *members* that exist: fields, properties, methods, and so on. For now, we've only characterized methods as code and fields as data but haven't classified properties yet. Conceptually, they're a way to expose data, although physically they're defined as operations (that is, code).

To be completely fair, a third element exists in this cocktail: *metadata*, which is data about the type and its members itself. Metadata has several roles. For starters, it enables the exploration of the capabilities of types at runtime using reflection, allowing questions to be asked (such as, "What are the methods on this type?") at runtime. Furthermore, certain kinds of members are fueled by metadata. For example, although properties look like a mechanism to expose data, they really consist of (pairs of) methods underneath. Using metadata, tools can explore the capabilities of types (for example, for IntelliSense) and receive guidance on how to consume the type (for example, use of a property getter corresponds to such a method call). Finally, metadata is a driver for certain runtime aspects. The canonical example is serialization, which can be turned on for a type using a custom attribute:

```
[Serializable]
class Person { /* ... */ }
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_494_0.png)

FIGURE 9.1 Decomposing a type.

Different sorts of types exist, two of which we look at in this chapter: classes and structs. Both provide containers for code and data, whereas some of the other types are exclusively focused on one aspect. For example, delegates and interfaces are all about operations you can perform, whereas enumerations are all about data that gets defined as named constants. Figure 9.2 illustrates where classes and structs live.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_494_1.png)

FIGURE 9.2 Where classes and structs are situated.

## Classes Versus Structs

Figure 9.2 illustrates where classes and structs fit in the sea of types that are available to managed code developers. You can debate where exactly in the diagram sorts of types belong, but let's accept my choice for now.

### References Versus Values

Struct is a fancy word for value type. Recall that value types are copied by value; every time an instance of a value type (sometimes abbreviated simply as value) is passed, a copy is created. This is in sheer contrast to reference types, where a reference to the object is passed along.

Let's concretize matters by considering integral numeric values. Why are those value types? There are a couple of reasons. First, values have some kind of immutable characteristic: 1 is 1 and will always be. Although immutability is not a requirement for value types, not obeying it is asking for trouble, as you will see. This doesn't mean a variable of a value type can't change (after all, isn't the point of a variable to vary?); all I'm saying is that the value itself can't change:

```
for (int i = 0; i < 10; i++)
    // Do something
```

Here, the value of variable i is changing all the time. However, the instances of the Int32 type are not changing: By incrementing 1, you're not affecting everyone who's using 1 somewhere. Even in natural language, this is reflected: When using the word one to mean a number, you're not referring to some magical instance of the number 1 kept in some central location (that one). And we deem it pretty unlikely a genius mathematician will come around anytime soon mandating a change to the number 1! Figure 9.3 contrasts the notion of a value with that of a reference.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_495_0.png)

FIGURE 9.3 Integral numbers are value types.

Another canonical example of a value type is a point. A point has different coordinates, like X and Y, but those are fixed. You might wonder: But what if something needs to be moved? What's changing is not the point's data itself, but rather the location of the object being moved. This location will be of type Point, and during a move it will get a different value assigned. Imagine that Point is a reference type and the following code sets the
