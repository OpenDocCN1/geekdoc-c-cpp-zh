```
// create a person with 180cm and 75kg
let p = Person(Height = 180.<cm>, Weight = 75.<kg>)

// perform the chain check
check p
```

Execution result
good, this person passes

# Working with the Adapter Pattern

The adapter pattern is a design pattern that translates one interface for a type into an interface that is compatible with some other type. In Listing 3-8, we use the Generic Invoke(GI) function as an adapter or bridge to invoke two methods of incompatible types. By using the GI, a common interface is no longer needed and the function can be invoked. The GI function is a static constraint, it requires that T define a certain member function. In Listing 3-7, it requires that the T has a CanConnect that takes void (unit) and returns a Boolean. (Note that F# you to declare a function as "inline" when arguments of the function are statically resolved type parameters as those in the following code listing)

+   LISTING 3-7 GI function

```
// define a GI function
let inline canConnect (x : ^AT) = (^AT : member CanConnect : unit->bool) x
```

The interesting about this design implementation in Listing 3-8 is that Cat and Dog do not have any common base class or interface. However they can still be processed in a unified function. This implementation can be used to invoke the legacy code, which does not share any common interface or base class. (You should note, by the way, that this is a sloppy way of solving the problem and should be considered only when no other option is available.)

Imagine that you have two legacy systems that need to be integrated and that you do not have access to the source code. It would be difficult to integrate the systems in other languages, but it's possible and even easy in F# using the generic invoke technique.