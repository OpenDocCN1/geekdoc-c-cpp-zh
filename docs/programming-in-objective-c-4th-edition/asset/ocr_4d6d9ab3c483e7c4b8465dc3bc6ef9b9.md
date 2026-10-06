outline msgs
...
}

The special @protocol directive as used here takes a protocol
name and produces a protocol object, which is what the
conformsToProtocol: method expects as its argument.

To test to see if currentObject has implemented the optional
outline method, you could write this:

```
if ([currentObject]) respondsToSelector:
@selector(outline)] == YES)
[currentObject outline];
```

You can enlist the aid of the compiler to check for conformance with
your variables by including the protocol name inside angular
brackets after the type name, like this:

```
id <Drawing> currentObject;
```

This tells the compiler that currentObject will reference objects
that conform to the Drawing protocol. If you assign a statically-
typ object to currentObject that does not conform to the
Drawing protocol (say that you have a Square class that does not
conform), the compiler issues a warning message that looks like this:

```
warning: class 'Square' does not implement the
'Drawing' protocol
```

This is a compiler check here, so assigning an id variable to
currentComponent would not generate this message because the
compiler has no way of knowing whether the object stored inside an
id variable conforms to the Drawing protocol.

You can list more than one protocol if the variable will hold an object
conforming to more than one protocol, as in this line: