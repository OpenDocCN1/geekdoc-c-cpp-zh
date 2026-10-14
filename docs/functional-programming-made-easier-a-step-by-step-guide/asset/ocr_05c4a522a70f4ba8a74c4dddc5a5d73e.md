```
data List a = Nil | Cons a (List a)
```

If we use the Data Constructor, Nil, we will construct a Type, List a. But what Type is a?

There is no way to tell.

If we look at the other test code line I gave you, we can determine List’s Type easily:

```
log $ show $ head ("abc" : "123" : Nil)
```

It’s Type is List String.

But with an empty List, there are no elements to interrogate. It could be a List of anything, viz. List a, where a is our anything. The problem is that the compiler wants to verify that a can be passed to show (more on that later).

How do we fix this then?

Type Inference infers what Types our values are by how we use them. But when there isn’t enough evidence, as in the case of our empty List, then we must explicitly specify the Type.

Here’s how to properly do that:

```
log $ show (head Nil :: Maybe Unit)
```

We parenthesize the call to head and specify an explicit Type for its return value. But why Unit as the List element Type?

It really doesn’t matter. It just needs any valid Type that we can show (more on that later). By using Unit, we are signaling to anyone reading our code that the element Type really doesn’t matter. Had we used Int or some other non-trivial Type, the reader of our code (which could very well be us some time in the future), may think there’s more to that list than meets the eye.

Returning to the error message for a minute:

```
No type class instance was found for Data.Show.Show t2
```

It’s worth noting that during Type Inference, the compiler will "lose" your names and create any unknown type names with a t and a number. Here it has come up with t2 for our a.

It can be very difficult from time to time to do that mapping between the type the compiler is referring to and what we called it. This is an understandable issue, since it may be referring to multiple Function, like, log, show and head which all call their Type Parameters a.