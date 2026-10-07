# Chapter 10 More on Variables and Data Types

A class that contains many methods and instance variables in it commonly has several initialization methods as well. For example, the Foundation framework's NSArray class contains the following six initialization methods:

```
initWithArray:
itWithArray:copyItems:
initWithContentsOfFile:
initWithContentsURL:
initWithObjects:
initWithObjects:count:
```

An array might be allocated and then initialized with a sequence like this:

```
myArray [[NSArray alloc] initWithArray:myOtherArray];
```

It's common practice for all the initializers in a class to begin with init...As you can see, NSArray's initializers follow that convention. You should adhere to the following two strategies when writing initializers.

If your class contains more than one initializer, one of them should be your designated initializer and all the other initialization methods should use it. Typically, that is your most complex initialization method (usually, the one that takes the most arguments). Creating a designated initializer centralizes your main initialization in a single method. Anyone subclassing your class can override your designated initializer, to ensure that instances are properly initialized.

+   Ensure that any inherited instance variables get properly initialized. The easiest way to do that is to first invoke the parent's designated initialization method, which is most often init. After that, you can initialize your instance variables.

Based on that discussion, your initialization method initWithWith:over: for your Fraction might look like this:

```
-(Fraction *) initWithWith:(int) n over:(int) d
{
  self [super init];

  if (self) {
    [self setTo:n over:d];
  }

  return self;
}
```

This method invokes the parent initializer first, which is NSObject's init method (recall that this is Fraction's parent). You must assign the result back to self because an initializer has the right to change or move the object in memory.

Following the initialization of super (and its success, as indicated by the return of a nonzero value) you use the setTo:over: method to set the numerator and denominator of your Fraction. As with other initialization methods, you are expected to return the initialized object, which you do here.