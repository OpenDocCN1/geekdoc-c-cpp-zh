the unsafe modifier specified in the struct declaration causes the entire textual extent of the struct declaration to become an unsafe context. Thus it is possible to declare the Left and Right fields to be of a pointer type. The example above could also be written as follows:

```
public struct Node
{
    public int Value;
    public unsafe Node* Left;
    public unsafe Node* Right;
}
```

Here, the unsafe modifiers in the field declarations cause those declarations to be considered unsafe contexts.

Other than establishing an unsafe context, thereby permitting the use of pointer types, the unsafe modifier has no effect on a type or a member. In the example

```
public class A
{
    public unsafe virtual void F() {
        char* p;
        ...
    }
}

public class B : A
{
    public override void F() {
        base.F();
        ...
    }
}
```

the unsafe modifier on the F method in A simply causes the textual extent of F to become an unsafe context in which the unsafe features of the language can be used. In the override of F in B, there is no need to re-specify the unsafe modifier—unless, of course, the F method in B itself needs access to unsafe features.

The situation is slightly different when a pointer type is part of the method's signature:

```
public unsafe class A
{
    public virtual void F(char* p) {...}
}

public class B : A
{
    public unsafe override void F(char* p) {...}
}
```

Here, because F's signature includes a pointer type, it can be written only in an unsafe context. However, the unsafe context can be introduced either by making the entire class