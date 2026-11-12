class or if you need to redefine methods in that class, you can form an **_is-a_ relationship** between your classes; that is, you can use private inheritance.

To derive Stack from List using private inheritance, you begin the definition of the class Stack with the header

```
class Stack : private List
```

List’s public members—and protected members, if List has any—would be private members of Stack. Thus, within the implementation of Stack, you would be able to use a List to store the stack’s entries and manipulate them by using List’s methods. We say that Stack implements the ADT stack **_as-a_** List. Both the descendants and clients of Stack are unable to access any members of List. Thus, the underlying list is hidden from the clients of the stack.

If public inheritance is inappropriate and your class does not need access to the protected members of another class, or if you do not need to redefine methods in that class, a **_has-a_** relationship is preferable and simpler to use. We consider that next.

# ## C4.2 Containment: Has-a Relationships

A ball-point pen **_has a_** ball as its point, as Figure C4-8 illustrates. Although you would want to use Ball in your definition of a class Pen, you should not use public inheritance, because a pen is not a ball. In fact, you do not use inheritance at all to implement a **_has-a_ relationship**. Instead, you can define a data member point—whose type is Ball—within the class Pen as

```
class Pen
{
    private:
        Ball point;
        ... // end Pen
};
```

Recall that any data member can be an instance of any class other than the one currently being defined— Pen, in this example. An instance of Pen has, or **_contains_**, an instance of Ball. Thus, another name for the **_has-a_** relationship is **containment**.

As you continue to examine the ball’s relationship to the pen, you may realize that if the pen is destroyed, the ball should also be destroyed, since it no longer has a purpose. When an instance of an object cannot exist independently of the containing class, this type of containment is called

Has-a, or containment, means a class has an object as a data member

# **FIGURE C4-8** A pen has a or contains a ball

![](bbox=[0.4, 0.69, 0.75, 0.9])