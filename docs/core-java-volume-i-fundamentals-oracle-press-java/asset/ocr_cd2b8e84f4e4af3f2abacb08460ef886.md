```
```java
void move(double x, double y);
}
```
```

Then, you could imagine an interface called Powered that extends it:

```
```java
public interface Powered extends Moveable
{
    double milesPerGallon();
}
```
```

Although you cannot put instance fields in an interface, you can supply constants in them. For example:

```
```java
public interface Powered extends Moveable
{
    double milesPerGallon();
    double SPEED_LIMIT = 95;  // a public static final constant
}
```
```

Just as methods in an interface are automatically public, fields are always public static final.

> **NOTE:**
> 
> It is legal to tag interface methods as public, and fields as public static final. Some programmers do that, either out of habit or for greater clarity. However, the Java Language Specification recommends that the redundant keywords not be supplied, and I follow that recommendation.

While each class can have only one superclass, classes can implement *multiple interfaces*. This gives you the maximum amount of flexibility in defining a class’s behavior. For example, the Java programming language has an important interface built into it, called cloneable. (This interface is discussed in detail in [Section 6.1.9, “Object Cloning,”](#) on p. 330.) If your