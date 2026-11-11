fields) are fine. Since out has been declared as final, you cannot reassign another print stream to it:

```
System.out = new PrintStream(...); // ERROR--out is final
```

> > **NOTE:** If you look at the System class, you will notice a method setOut that sets System.out to a different stream. You may wonder how that method can change the value of a final variable. However, the setOut method is a native method, not implemented in the Java programming language. Native methods can bypass the access control mechanisms of the Java language. This is a very unusual workaround that you should not emulate in your programs.

# 4.4.3 Static Methods

Static methods are methods that do not operate on objects. For example, the pow method of the Math class is a static method. The expression

Math.pow(x, a)

computes the power xᵃ. It does not use any Math object to carry out its task. In other words, it has no implicit parameter.

You can think of static methods as methods that don’t have this parameter. (In a nonstatic method, the this parameter refers to the implicit parameter of the method—see Section 4.3.7, “Implicit and Explicit Parameters,” on p. 150.)

A static method of the Employee class cannot access the id instance field because it does not operate on an object. However, a static method can access a static field. Here is an example of such a static method:

```
public static int getNextId()
{
    return nextId; // returns static field
}
```

To call this method, you supply the name of the class:

```
int n = Employee.getNextId();
```

Could you have omitted the keyword static for this method? Yes, but then you would need to have an object reference of type Employee to invoke the method.