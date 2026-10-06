Now, what do you think would happen if the program later changed some of the characters contained in newName in the program (this could happen if newName were a mutable string object; such an object can be used in places where an NSString object is specified, as the former is a subclass of the latter?) It would also unintentionally change the corresponding field in your address card because both would reference the same string object.

As you have already seen, a safer approach is to make a copy of the object in the setter to prevent this inadvertent effect.

If you're synthesizing the setter, you could also write a version of the setName: method to use copy, like this:

```
- (void) setName: (NSString *) theName
{
    name = [theName copy];
}
```

As you saw in Chapter 15, "Numbers, Strings, and Collections," if you specify the copy attribute in a property declaration, the synthesized method will use the class's copy method (the one you wrote or the one you inherited). So the following property declaration

@property (nonatomic, copy) NSString *name;

when combined with the appropriate @synthesize directive, will generate a method that behaves like this:

```
- (void) setName: (NSString *) theName
{
    if (theName != name)
        name = [theName copy];
}
```