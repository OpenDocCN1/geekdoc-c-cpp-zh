Depending on what the state of the Boolean variable, isSubtractionWayBetterThanAddition, is, we could end up by calling our subtract method.

# Methods as First-Class Citizens

You might have realized that using a delegate is very much like using a variable or an object and this is done by design.

A delegate lets you assign a method as you do with a variable; it lets you pass a method as a parameter to another method and it lets you return a method from another method.

In computer programming, this has a name. A delegate will make it so that a method is a “first-class citizen”, much like the variables with a value type – the int, float, byte, etc. – and the structs and objects.

This is a very powerful ability but only if you know exactly how to use it. Later, in the next part of this guide, we’ll be discussing events and these are also very useful, especially to those who want to get involved in GUI programming and create much better interfaces than the console.

Aside from that, delegates are incredibly powerful all by themselves and that makes them worth knowing about.

# A Better Example

Just to show you, once and for all, the power and usefulness that delegates have, I’m going to show you a more complex example; this is very powerful and it is likely to confuse you.

But, I will tell you this. If you have kept up with me so far and you have a basic understanding of everything to this point if you feel that you are truly ready to move on and look at events, then understanding this part really isn’t that critical. If you want, you can move on to events right now but I would suggest that you finish this section, if only to round off your knowledge.

Let’s start by looking at exactly what we aim to achieve with this example. Let’s assume that you have an object, anything, it doesn’t matter what it is, and you are using this object. You also have a List,