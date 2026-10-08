24 CHAPTER 2: An Objective-C Primer

Objective-C headers.¹1 The SEL type is used for selectors, which we'll look at later in this chapter.

The last one is IMP, which stands for Instance Method Pointer. This type refers to a pointer to an Objective-C method. Most of the time, you won't need to use this type at all. It is only used for some of the very dynamic features of Objective-C, and for optimization. We'll look at some places where you might use it in Chapter 19.

# Sending Messages

```
[anObject autorelease];
[anObject addObject:anotherObject];
[anObject setObject:anotherObject
key:aThirdObject];
```

From: exampleMessages.m
The most important addition to C that Objective-C makes sending messages. A message, as I said in the last chapter, is a high-level flow control construct.

This is the bit of Objective-C that tends to intimidate people coming from languages such as C++ and Java, because the syntax is taken straight from Smalltalk and looks quite alien to people more familiar with C syntax. This is

¹If you are compiling with Clang, most of these types have built-in definitions, so the headers are optional.