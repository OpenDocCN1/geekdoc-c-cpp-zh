For added clarity, a class with one or more abstract methods must itself be declared abstract.

```
```java
public abstract class Person
{
    . . .
    public abstract String getDescription();
}
```
```

In addition to abstract methods, abstract classes can have fields and concrete methods. For example, the Person class stores the name of the person and has a concrete method that returns it.

```
```java
public abstract class Person
{
    private String name;
    public Person(String name)
    {
        this.name = name;
    }
    public abstract String getDescription();
    public String getName()
    {
        return name;
    }
}
```
```

![](bbox=[0.128, 0.704, 0.181, 0.747])

> **TIP:**
> 
> Some programmers don’t realize that abstract classes can have concrete methods. You should always move common fields and methods (whether abstract or not) to the superclass (whether abstract or not).