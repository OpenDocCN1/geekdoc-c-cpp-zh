96 CHAPTER 4: Common Objective-C Patterns

# Supporting Two-Stage Creation

```
NSMutableString *buffer =
  [[MutableString alloc] init];
NSMutableArray *array =
  [[NSMutableArray alloc]
    initWithObject: buffer];
```

From: allocInit.m

One of the patterns you've probably already seen is the two-stage creation pattern. In traditional, pre-NeXT, Objective-C, you create an object by sending the class a +new message. When you implemented a new class, you would override +new to call the superclass implementation and then perform that class's initialization.

NeXT changed this, splitting object creation and object initialization into two different methods. The +new method still works, but now it sends a +alloc message to the class and a -init message to the returned object.

The +alloc method itself, by default, calls +allocWithZone:. This takes an NSZone as an argument. This is an opaque type encapsulating an allocation zone. This was used very heavily on NeXT systems, to make efficient use of the very small amount of memory that these machines came with. It does not work particularly well on OS X, and is not properly supported by all classes, so it's something of a vestigial feature in a lot of modern Objective-C code.