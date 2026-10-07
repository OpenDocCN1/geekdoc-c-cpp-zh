# CHAPTER 2
Cocoa Objects

As with function parameters, the type of parameter must match the type specified in the method declaration. as an example the following message expression from SimpleCocoaTool:

```
objectivec\NSCountedSet *cset = [[NSCountedSet alloc] initWithArray:param];
```

Here param, which is also an instance of the NSArray class, is the parameter of the message named initWithArray.

The initWithArray: example cited above is interesting in that it illustrates nesting. With Objective-C, you can nest one message inside another; the object returned by one message expression is sent to the receiver by the message expression it encloses. To interpret nested message expressions, start with the inner expression and work your way out. The interpretation of the statement would be:

+   1. The alloc message is sent to the NSCountedSet class, which creates (by allocating memory for it) an uninitialized instance of the class.

> Note: Objective-C classes are objects in their own right and can send messages to them as well as their instances. In a message expression, the receiver of a class message is always a class object.

+   2. The initWithArray message is sent to the uninitialized instance, which initializes it with the array args and returns a reference to it.

Next consider this statement from the main routine of SimpleCocoaTool:

```
objectivec
NSArray *sorted_args = [[NSArray alloc]
sortedArrayUsingSelector:selector(compare:)];
```

What's noteworthy about this message expression is the parameter of the sortedArrayUsingSelector message. This parameter requires the use of the @selector compiler to create a selector to be used as a parameter.

Let's pause a moment to review message and method methodology. A message is essentially a function defined and implemented by the class of which the receiver of a message is a member. A message is a selector name (perhaps consisting of one or more keys) along its parameters; a message is sent to a receiver and results in the invocation (or execution) of the method. A message expression encompasses both receiver and message. Figure 2-2 depicts these relationships.

# Figure 2-2 Message expression

![](bbox=[0.178, 0.702, 0.556, 0.831])

Objective-C uses a number of defined types and literals that you won't find in ANSI C. In some cases, these types and literals replace their ANSI C counters. Figure 2-2 describes a few of the important ones, including the allowable literals for each type.

Oriented Programming with Objective-C 65
2010-12-13 | 2010 Apple Inc. All Rights Reserved.