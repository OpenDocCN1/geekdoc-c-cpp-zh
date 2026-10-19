# Good Encapsulation

As Section 5.3 discussed, encapsulation is a stronger concept than abstraction. Abstraction helps to manage complexity by providing models that allow you to ignore implementation details. Encapsulation is the enforcer that prevents you from looking at the details even if you want to.

The two concepts are related because, without encapsulation, abstraction tends to break down. In my experience, either you have both abstraction and encapsulation or you have neither. There is no middle ground.

**Minimize accessibility of classes and members** Minimizing accessibility is one of several rules that are designed to encourage encapsulation. If you’re wondering whether a specific routine should be public, private, or protected, one school of thought is that you should favor the strictest level of privacy that’s workable (Meyers 1998, Bloch 2001). I think that’s a fine guideline, but I think the more important guideline is, “What best preserves the integrity of the interface abstraction?” If exposing the routine is consistent with the abstraction, it’s probably fine to expose it. If you’re not sure, hiding more is generally better than hiding less.

**Don’t expose member data in public** Exposing member data is a violation of encapsulation and limits your control over the abstraction. As Arthur Riel points out, a *Point* class that exposes

```
float x;
float y;
float z;
```

is violating encapsulation because client code is free to monkey around with *Point*’s data and *Point* won’t necessarily even know when its values have been changed (Riel 1996). However, a *Point* class that exposes

```
float GetX();
float GetY();
float GetZ();
void SetX( float x );
void SetY( float y );
void SetZ( float z );
```

is maintaining perfect encapsulation. You have no idea whether the underlying implementation is in terms of *floats* x, y, and z, whether *Point* is storing those items as *doubles* and converting them to *floats*, or whether *Point* is storing them on the moon and retrieving them from a satellite in outer space.

**Avoid putting private implementation details into a class’s interface** With true encapsulation, programmers would not be able to see implementation details at all. They would be hidden both figuratively and literally. In popular languages, including

> The single most important factor that distinguishes a well-designed module from a poorly designed one is the degree to which the module hides its internal data and other implementation details from other modules.
> 
> —Joshua Bloch

**Cross-Reference** For more on encapsulation, see “Encapsulate Implementation Details” in Section 5.3.