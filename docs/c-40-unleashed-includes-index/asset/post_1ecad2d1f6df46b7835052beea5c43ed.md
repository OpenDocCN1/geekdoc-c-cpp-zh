
In today's world, whenever I see such direct use of System.Object in freshly written code, I get a bit nervous. As you get to know generics and dynamic better in the following chapters, you should start feeling the same way. I think the time has come to consider System.Object more of an implementation detail of the CLR type system rather than a type amenable for direct use.

Declaring objects with the System.Object type is just one side of the coin, though. An equally important perspective is that of using the operations defined on System.Object. All types inherit those commonly used methods whose role we discuss in more detail in Chapter 13, “Operator Overloading and Conversions.” Here they are to set the scene:

- Equals compares the instance against another object for equality.
- GetHashCode calculates a hash code for the instance. Hash codes are used to store and retrieve objects efficiently in certain collection types.
- ToString provides a string representation of the instance.

Note that these three methods are all virtual, meaning derived types can (and often do) override them to provide a specialized meaning. We discuss what these terms mean when we cover OOP in Chapter 14.

All things being equal, should you still care about System.Object that much? It's without a doubt a good thing to know about its role in the type hierarchy and to see it as an ultimate resort for generic programming if—for some very rare reason—generics don't apply in some circumstance. But nowadays, the most common use of System.Object should likely be in the use of methods like ToString and Equals.

## Dynamic Typing

![](img/a16f85e62ce9bdc527f4b09dbfe26092_230_0.png)

Starting with .NET 4.0, C# supports dynamic typing. Variables typed as dynamic are used in a late-bound fashion, meaning that operations applied to them are resolved at runtime rather than at compile time. This is useful when dealing with an object that cannot be typed statically in a comfortable manner. Samples include XML documents without an XSD schema or objects from dynamic languages such as Python, Ruby, or JavaScript.

Other than the built-in types we've seen so far, there's no direct mapping between the C# reserved word dynamic and an underlying BCL type. Instead, dynamic is a special alias for System.Object, but with some additional metadata sprinkled on top of it to tell the compiler to emit late-bound code. This makes a lot of sense actually: The “minimal” static type in the CLR is System.Object; you can't sink lower. By typing it as dynamic, you're essentially saying this: Dear compiler. Trust me, I'm confident that the operations I carry out will make sense at runtime. So don't waste your time trying to verify those statically at compile time.

```
object o = GetSomething();
o.DoSomething(); // compile-time error; System.Object does not have DoSomething

dynamic d = GetSomething();
d.DoSomething(); // check for the presence of DoSomething at runtime
```

## Compile Time Type Versus Runtime Type

To make things a bit more concrete, assume a PetShop object defines a method called GetPromotionOfTheDay whose return type is Animal. Different subtypes exist for Animal, such as GoldFish and Canary. There can even be more structure with intermediate types, such as Fish and Bird. We'll look at OOP in the later chapters, but you get the idea.

Statically (a compile-time thing), all we know about GetPromotionOfTheDay is that it returns an animal. Before driving to the shop to get the animal (a runtime thing), we can't know what we'll get back, assuming we didn't hear about the type of the promotion in any way. At this point, we can make a few assumptions about the things we'll be able to do with the animal. Walk (a method call) won't apply very well if we get back with a fish, and it's way too dangerous trying to Bathe (another method call) a cat. Maybe the only thing we can be sure about is to Watch it.

Dynamically (a runtime thing), though, the animal we get back will have a concrete type. It might be a dog, a goldfish, or whatnot. Now it makes sense to Walk the dog or to Bathe the goldfish and so on. But there was no way we could have known before obtaining the animal. We're using dynamic knowledge obtained in the act of getting the shop's promotion of the day.

Now let's assume through some magical powers you happen to know that the PetShop's GetPromotionOfTheDay always returns a mammal (and doesn't have the space to have a whale in stock). As far as I know, all mammals except for whales can walk (but I'm not an expert), so it will always be safe to call Walk on our purchased animal. From a statically typed perspective, we can't know this (a compile-time error), but given the additional information we got somehow, we can treat the animal dynamically and call Walk on it anyway. Figure 4.16 contrasts static and dynamic typing.

I detail the innards of dynamic typing and how to use and extend it in Chapter 22, “Dynamic Programming.” With this, we conclude our journey through built-in types the C# language knows about by means of reserved words.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_232_0.png)

FIGURE 4.16 Static typing versus dynamic typing.

## A Word on CLS Compliance

Chapter 1, “Introducing the .NET Platform,” stressed the importance of cross-language interoperability in the vision statement of .NET. One key criterion for success in this space is ensuring that types created in one language can be used or extended from another language. This is where the Common Language Specification (CLS) comes into play.

Before delving any deeper, let's revisit the first rule of the CLS:

> CLS Rule 1: CLS rules apply only to those parts of a type that are accessible or visible outside of the defining assembly.

We haven't talked about visibility yet, but the idea is rather simple. Assemblies contain types, some of which can be exposed to the outside world. A similar observation holds for types in relation to their members. Some members, such as fields or methods, are for exclusive use by the type's code, whereas others are part of the type's contract and hence exposed to others.

The first CLS rule states an obvious fact: To be cross-language-compatible, only those parts of a type that are accessible or visible outside the defining assembly matter. In other words: Do whatever you like on the inside, but stand still for a few seconds when you touch the outside.

## SHOULD I CARE?

Applications are often written by separating out certain functionality into helper libraries, with the idea of code sharing in mind or for architectural cleanliness. It's sometimes tempting to say you will always be the only one using that library, and you'll always use C# for the job at hand. So why should you care about making the assembly CLS-compliant?

This naive assumption can pose a serious risk when the unexpected happens, requiring you or someone else to reach out to the non-CLS-compliant library. Maybe a new developer has been hired who's fluent in another .NET language, or your firm has decided to jump on the bandwagon of functional languages. Or you find yourself in a situation where you want to call some of your library functionality from an interactive prompt of some dynamic language.

For all those reasons, the first thing I do for 99% of my projects is to turn on CLS-compliance checking. By doing so, I avoid trying to tweak a library into becoming CLS-compliant and thus potentially breaking others that already rely on some of the noncompliant public APIs. In general, I find the act of ensuring CLS compliance not something that disturbs development workflow, and when a CLS compliance warning is raised, I've learned something new about the platform. A win-win situation, if you ask me.

How to turn on CLS compliance checking? In essence, you just state that you ensure the assembly is CLS-compliant, causing the C# compiler to carry out CLS-specific checks when dealing with publicly visible stuff. To declare an assembly CLS compliant, an assembly-level attribute is used. In Visual Studio, you can find those declared in a file called AssemblyInfo.cs under the Properties node for the project in Solution Explorer. Figure 4.17 shows where to find the AssemblyInfo.cs file.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_233_0.png)

FIGURE 4.17 Locating the AssemblyInfo.cs file in a C# project.

Open this file and browse around a bit to get a feeling about what information an assembly can carry. Hover over the various attributes to see a brief explanation of their goals. Most of those can be configured through the user interface, as you will see later. To make the assembly CLS-compliant and to have the compiler check this claim, add the following line somewhere in the file (at the bottom will do):

```
[assembly: CLSCompliant(true)]
```

The square bracket syntax is used for attributes, pieces of metadata that can be sprinkled on top of various program entities. For example, to make a type serializable for storage on
