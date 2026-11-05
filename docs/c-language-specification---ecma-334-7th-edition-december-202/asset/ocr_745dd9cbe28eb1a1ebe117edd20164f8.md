```
class Base
{
    public void F() {}
}
class Derived : Base
{
    public void F() {} // Warning, hiding an inherited name
}
```

the declaration of F in Derived causes a warning to be reported. Hiding an inherited name is specifically not an error, since that would preclude separate evolution of base classes. For example, the above situation might have come about because a later version of Base introduced an F method that wasn't present in an earlier version of the class.

end example

The warning caused by hiding an inherited name can be eliminated through use of the new modifier:

Example:

```
class Base
{
    public void F() {}
}
class Derived : Base
{
    public new void F() {}
}
```

The new modifier indicates that the F in Derived is “new”, and that it is indeed intended to hide the inherited member.

end example

A declaration of a new member hides an inherited member only within the scope of the new member.

Example:

```
class Base
{
    public static void F() {}
}
class Derived : Base
{
    private new static void F() {} // Hides Base.F in Derived only
}
class MoreDerived : Derived
{
    static void G()
    {
        F();            // Invokes Base.F
    }
}
```