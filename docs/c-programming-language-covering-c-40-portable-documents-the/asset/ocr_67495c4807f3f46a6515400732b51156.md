```
{
    public void G() {}
}
class C: B
{
    public override void F() {
        // Actual implementation of F
    }
}
```

the abstract class A introduces an abstract method F. Class B introduces an additional method G, but since it doesn't provide an implementation of F, B must also be declared abstract. Class C overrides F and provides an actual implementation. Since there are no abstract members in C, C is permitted (but not required) to be nonabstract.

# 10.1.1.2 Sealed Classes

The sealed modifier is used to prevent derivation from a class. A compile-time error occurs if a sealed class is specified as the base class of another class.

A sealed class cannot also be an abstract class.

The sealed modifier is primarily used to prevent unintended derivation, but it also enables certain runtime optimizations. In particular, because a sealed class is known to never have any derived classes, it is possible to transform virtual function member invocations on sealed class instances into nonvirtual invocations.

> JON SKEET  The choice to make classes unsealed (but methods nonvirtual) by default has always been a hotly disputed one. I agree with the maxim “Design for inheritance or prohibit it,” but there are arguments both ways. The odd point is how powerful a default is: Even though I usually choose to seal classes if I think about it, it’s all too easy to ignore the choice entirely. It obviously doesn’t affect what can be expressed, but I’m certain it affects the code that is actually produced.

> JESSE LIBERTY  I will take the risk of disagreeing with Jon.
> 
> It is demonstrably false that you can accurately anticipate what will be needed even months in advance. Thus good programming practice would dictate letting your design emerge, building little or nothing before it is explicitly needed, and avoiding closing off avenues you believe you’ll never need.
> 
> Sealed is a minefield laid down to state, “You’ll never need to go here.” I don’t think you can know that or should presume to try.