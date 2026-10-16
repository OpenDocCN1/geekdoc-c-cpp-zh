# Avoiding Circular Protocol Dependencies

Protocols can refer to other protocols within their own declarations. For example, imagine a protocol which requires another protocol for use as a parameter to one of its methods, as shown in Listing 7.8.

# Listing 7.8

# A protocol requiring another protocol

```
@protocol Foo
- (void) someMethodRequiringBar: (id<Bar>) inBar;
@end
```

If the required protocol (Bar) also requires the original protocol (Foo), as shown in Listing 7.9, then a circular dependency is created between the two protocols. This generates a compiler error.

# Listing 7.9

# The Bar protocol, which requires the Foo protocol

```
@protocol Bar
- (void) someMethodRequiringFoo: (id<Foo>) inFoo;
@end
```

To resolve this problem, you can give a forward declaration of the required protocol which enables you to not include the file for the protocol that is required. For example, to prevent this circular dependency, you can add to the Bar.h interface file, the directive @protocol Foo; instead of importing the Foo.h file. This is shown in Listing 7.10.

# Listing 7.10

# A corrected version of the Bar protocol.

```
@protocol Foo;
@protocol Bar
- (void) someMethodRequiringFoo: (id<Foo>) inFoo;
@end
```