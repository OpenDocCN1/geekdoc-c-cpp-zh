would recursively invoke the PrintFields method declared in B, not the one declared in A, since PrintFields is virtual and the runtime type of ((A)this) is B.

Only by including an override modifier can a method override another method. In all other cases, a method with the same signature as an inherited method simply hides the inherited method. In the example

```
```
class A
{
    public virtual void F() { }
}

class B: A
{
    public virtual void F() { }        // Warning: hiding inherited F()
}
```
```

the F method in B does not include an override modifier and, therefore, does not override the F method in A. Rather, the F method in B hides the method in A, and a warning is reported because the declaration does not include a new modifier.

In the example

```
```
class A
{
    public virtual void F() { }
}

class B: A
{
    new private void F() { }        // Hides A.F within body of B
}

class C: B
{
    public override void F() { }    // Okay: overrides A.F
}
```
```

the F method in B hides the virtual F method inherited from A. Since the new F in B has private access, its scope includes only the class body of B and does not extend to C. Therefore, the declaration of F in C is permitted to override the F inherited from A.

# ### 10.6.5 Sealed Methods

When an instance method declaration includes a sealed modifier, that method is said to be a *sealed method*. If an instance method declaration includes the sealed modifier, it must also include the override modifier. Use of the sealed modifier prevents a derived class from further overriding the method.