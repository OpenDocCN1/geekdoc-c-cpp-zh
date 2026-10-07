subclass from overriding a base class member that was originally declared as virtual higher in the inheritance chain. Such a situation arises when a subclass B overrides a base class A's member and then needs to prevent any further overriding below subclass B.

LISTING 7.13: Sealing Members

```
class A
{
    public virtual void Method()
    {
    }
}
class B : A
{
    public override sealed void Method()
    {
    }
}
class C : B
{
    // ERROR: Cannot override sealed members
    //public override void Method()
    //{
    //}
}
```

In this example, the use of the sealed modifier on class B's Method() declaration prevents class C from overriding Method().

In general, marking a class as sealed is rarely done and should be reserved only for those situations in which there are strong reasons favoring such a restriction. For, leaving types unsealed has become increasingly desirable as unit testing has assumed greater prominence, because of the need to support mock (test double) object creation in place of real implementations. One possible scenario in which sealing a class might be warranted when the cost of sealing individual virtual members outweighs the benefits of leaving the class unsealed. However, a more targeted sealing of individual members—perhaps because of dependencies in the