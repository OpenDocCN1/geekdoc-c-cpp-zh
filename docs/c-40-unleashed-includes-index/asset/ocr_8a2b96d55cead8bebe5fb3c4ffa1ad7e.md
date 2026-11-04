# NOTE

In the preceding code snippet, I’m using a bunch of language features we haven’t looked at yet. In particular, on the first line you can see a collection initializer. Line two contains a cast expression and use of an indexer, and line three makes a method call. Don’t worry, we cover all of these in quite some detail as we move forward.

Earlier, I used the word *generic* in a rather ad hoc fashion. The use of `System.Object` for collection types wasn’t ideal for various reasons that will become apparent later, but the biggest stumbling block is the potential for users to make silly mistakes (as illustrated in the code fragment). Suppose you’re using an `ArrayList` to store integer values. Because `ArrayList` is defined to be able to deal with any kind of object, however, nothing prevents you from storing an object of another type, such as a string, in the same collection. In addition, there are performance implications associated with this approach (due to *boxing*, as you will see).

![](bbox=[0.085, 0.408, 0.141, 0.454])

To address that, .NET 2.0 introduced the concept of *generic types*, which we pay much more attention to in Chapter 15, “Generic Types and Methods.” One of the key properties of generic types is that they make excessive use of `System.Object` go away, essentially improving static typing and reducing typical silly mistakes that would otherwise be caught only at runtime:

```
```csharp
List<int> primes = new List<int> { 2, 3, 5, 7, 11 };
int two = primes[0];
primes.Add("thirteen"); // compile-time error!
int thirteen = primes[5];
```
```

# BANNING SYSTEM.OBJECT?

A colleague of mine—the ultimate native code and COM geek—told me about his first encounter with the .NET Framework in the 1.0 days. Although new runtimes like the CLR promised heaven on earth for type-safe code and promoted the use of static typing, you can guess his reaction when seeing a big number of casts in managed code. When I asked about the nature of that code, he recollected the everywhere use of collection types. That explained his original surprise, which resulted from the lack of generics in the early days of the CLR.

As time goes on, the number of scenarios requiring direct use of `System.Object` keeps decreasing. And by direct use I mean explicit declaration of variables of type `object`. With .NET 2.0, generics were introduced to improve static typing, and in .NET 4.0 a new dynamic type was introduced to deal with dynamic typing in a more explicit fashion than plain use of `System.Object`.