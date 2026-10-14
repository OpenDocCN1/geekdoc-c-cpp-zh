```
public int Red => Color.Red;
public int Green => Color.Green;
public int Blue => Color.Blue;
}
```

*Listing 7-18: Containing Color rather than inheriting from it*

Here, the compiler provides the implementation for IEquatable<T> for each type, leaving us to define just the properties and behavior for them. The TranslucentColor type contains a read-only Color instance, and we add a new constructor as a convenience for our users, who can either create a new Color value to pass to TranslucentColor's generated constructor or call our new constructor with each component part separately. We also mirror Color's properties in TranslucentColor and forward them to the contained Color value. We don't get those properties for free, but they afford users of TranslucentColor a much more natural interface, like this:

```
var bg = new TranslucentColor(0xFF, 0xA0, 0, 0x77);

Assert.That(bg.Red,  Is.EqualTo(0xFF));
Assert.That(bg.Green, Is.EqualTo(0xA0));
Assert.That(bg.Blue,  Is.EqualTo(0));
Assert.That(bg.Alpha, Is.EqualTo(0x77));
--snip--
```

The alternative would force users to explicitly obtain the Color property in order to access its properties, like so:

```
Assert.That(bg.Color.Red,  Is.EqualTo(0xFF));
Assert.That(bg.Color.Green, Is.EqualTo(0xA0));
Assert.That(bg.Color.Blue,  Is.EqualTo(0));

Assert.That(bg.Alpha,      Is.EqualTo(0x77));
--snip--
```

Whether we use structs or define our value types with sealed records or classes, or record structs, testing our new types is much simpler to reason about now, as we don't need to consider cases where TranslucentColor instances are referred to by Color references. That in itself is a large consideration because those tests will be not only easier to write but also easier to read by the next programmers who visit the code.

Composing types isn't a perfect match for the version that employed inheritance, because we can't use a TranslucentColor instance as an argument to a method expecting a Color. As you've seen, sometimes that substitutability isn't appropriate.

Inheritance isn't the only form of polymorphism nor the only mechanism that exhibits type substitutability, but other approaches allow the compiler to inform us when we incorrectly substitute one type for another. Let's take a look at some of them.