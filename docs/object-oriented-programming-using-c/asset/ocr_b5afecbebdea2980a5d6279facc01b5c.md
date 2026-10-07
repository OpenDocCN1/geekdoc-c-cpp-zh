# Object Oriented Programming using C#

Answer: It's an object which supports (at least) the operations:

```
void SellCopy()
 ToString()
```

and it has properties that allow us to
set the price,
get the number of copies
set the number of copies.

Inheritance guarantees that objects of any subclass of Publications provides at least these.

Note that a subclass can never remove an operation inherited from its superclass(es) – this would break the guarantee. Because subclasses extend the capabilities of their superclasses, the superclass functionality can be assumed.

It is quite likely that we would choose to override the ToString() method (initially defined within 'Object') within Publication and override it again within Magazine so the String returned provides a better description of Publications and Magazines. However we should not override the ToString() method in order to return the price – this would be changing the functionality of the method so that the method performs an inherently different function. Doing this would break the substitutability principle.

# 4.3 Polymorphism

Because an instance of a subclass is an instance of its superclass we can handle subclass objects as if they were superclass objects. Furthermore a superclass guarantees certain operations in its subclasses we can invoke those operations without caring which subclass the actual object is an instance of.

This characteristic is termed 'polymorphism', originally meaning 'having multiple shapes'.

Thus a Publication comes in various shapes ... it could be a Book, Magazine or DiscMag. We can invoke the SellCopy() method on any of these Publications irrespective of their specific details.

Polymorphism is a fancy name for a common idea. Someone who knows how to drive can get into and drive motor cars because they have a set of key characteristics – steering wheel, gear pedal, pedals for clutch, brake and accelerator etc – which the driver knows how to. There will be lots of differences between any two cars, but you can think of them as subclasses of a subclass which defines these crucial shared 'operations'.

If 'p' is a Publication, it might be a Book or a Magazine or a DiscMag.

Whichever it we know that it has a SellCopy() method.

So we can invoke p.SellCopy() without worrying about exactly 'p' is.