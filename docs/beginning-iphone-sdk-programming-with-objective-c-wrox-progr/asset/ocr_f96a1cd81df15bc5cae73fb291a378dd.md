Note that in the initWithName:andRate: initializer implementation, you first call the init initializer of the super (base) class so that its base class is properly initialized, which is necessary before you can initialize the current class:

```
- (id)initWithName:(NSString *) n andRate:(float) r
{
    if (self = [super init]) {
        //...
        //...
    }
    return self;
}
```

The rule for defining an initializer is simple: If a class is initialized properly, it should return a reference to self (hence the id type). If it fails, it should return nil.

For the initWithName: initializer implementation, notice that it calls the initWithName:andRate: initializer:

```
- (id)initWithName:(NSString *) n
{
    return [self initWithName:n andRate:0.0f];
}
```

In general, if you have multiple initializers, each with different parameters, you should chain them by ensuring that they all call a single initializer that performs the call to the super class's init initializer. In Objective-C, the initializer that performs the call to the super class's init initializer is called the designated initializer.

> NOTE As a general guide, the designated initializer should be the one with the greatest number of parameters.

To use the initializers, you can now call them during instantiation time:

```
SomeClass *sc1 = [[SomeClass alloc] initWithName:@"Wei-Meng Lee" andRate:35];
SomeClass *sc2 = [[SomeClass alloc] initWithName:@"Wei-Meng Lee"];
```

# MEMORY MANAGEMENT

Memory management in Objective-C programming (especially for iPhone) is a very important topic that every iPhone developer needs to be aware of. As do all other popular languages, Objective-C supports garbage collection, which helps to remove unused objects when they go out of scope and hence releases memory that can be reused. However, because of the severe overhead involved in implementing garbage collection, the iPhone does not support garbage collection. This leaves you, the developer, to manually allocate and de-allocate the memory of objects when they are no longer needed. This section discusses the various aspects of memory management on the iPhone.