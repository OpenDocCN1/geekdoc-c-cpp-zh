like Either and Try, in addition to Option. Functional error handling is the topic of Chapter 13.

In the code example, flatMap is used to apply transformations that might fail to outputs of previous computations, which might also have failed. You can use a similar strategy to transform asynchronous computations using transformations that can themselves be asynchronous by using flatMap to avoid nesting futures. This will be explored in Part II of the book (contrast Listing 10.5 with Listing 26.9, for instance).

Another area where flatMap is handy is reactive programming organized in terms of streams of events. While map is limited to a one-to-one mapping, flatMap is not. In particular, when an event is processed, it can be entirely consumed (triggering no further events), or it can trigger exactly one event, or it can trigger multiple events. By using flatMap instead of map, you avoid nesting streams of events, in the same way you avoid nesting options when dealing with missing values, or nesting futures when dealing with asynchronous computations (see Listing 27.9 for an illustration).

Indeed, flatMap is such a fundamental operation that it has its own underlying theory (monads), and Scala defines convenient syntax to organize flatMap-based computations (see Section 10.9).

# Aside on Functors and Monads

More than five minutes of browsing on the topic of functional programming is likely to bring you in contact with two intimidating words: functor and monad. These terms have their origin in category theory. The simplest definitions are as follows: A functor is a structure that implements map, and a monad is a structure that implements flatMap.

Technically, the map and flatMap functions need to satisfy a few properties for functors and monads to qualify as such. These properties are generic for all functors and all monads, and are expressed here in terms of a functor F and a monad M. Think of F[A] and M[A] as types like List[A] or Option[A]. For F to be a functor, the map method on F[A] must have the following signature:

```
def map[B](f: A => B): F[B] = ...
```

It must also satisfy the two following properties on every struct of type F[A]:

```
struct == struct.map(identity)
// or equivalently: struct == struct.map(x => x)
struct.map(f).map(g) == struct.map(f andThen g)
// or equivalently: struct.map(f).map(g) == struct.map(x => g(f(x)))
```

The first property states that mapping the identity function has no effect. The second property requires that map preserves function composition: Mapping f