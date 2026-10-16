injected to the Union type. But we can eliminate disjunction indirectly over a third type C in the Following way:

![](bbox=[0.34, 0.15, 0.66, 0.24])

or with an alternative notation:

![](bbox=[0.37, 0.3, 0.63, 0.34])

This states that if we have a proof that gives us a C from an A (A→C) and a proof that gives us a C from a B, (B→C), and we have either of A or B, (A∨B) then we can deduce C.

# 3.4 Extending Union Types

We will see in this book some ways to add behavior on Union types as we go along but for now let us see the default way: using polymorphism.

As i mentioned previously, If we want to add a new property/method to a Union of types, we must add the variations of the property/method in all the sub-types that can be in the Union. This is the use of default polymorphism in order to discriminate between the parts of the union:

```
public class Cons<T> : ListBase<T>
{
    ...
    public override T Multiply() => Value * Rest.Multiply();
}
```

```
public class Empty<T> : ListBase<T>
{
    ...
    public override T Multiply() => 1;
}
```

Here we have added Multiply in both parts of the union.