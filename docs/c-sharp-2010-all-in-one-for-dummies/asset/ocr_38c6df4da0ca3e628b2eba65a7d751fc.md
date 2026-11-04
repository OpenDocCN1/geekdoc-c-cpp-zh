```
```java
public class Robot
{
    private IPropulsion _propel;    //<--Notice the interface type here.
    // Somehow you supply a concrete propulsion object at runtime ...
    // Other stuff and then:
    public void Move(int speed, int direction)
    {
        // Use whatever concrete propulsion device is installed in _propel.
        _propel.Movement(speed, direction); // Delegate to its methods.
    }
}
```
```

Robot's Move() method delegates the real work to the object referred to through the interface. Be sure to provide a way to install a concrete Motor or Engine or another implementer of IPropulsion in the data member. Programmers often install that concrete object — “inject the dependency” — by passing it to a constructor:

```
```java
Robot r = new Robot(someConcreteMotor);   // Type IPropulsion
```
```

or by assigning it via a setter property:

```
```java
r.PropulsionDevice = someConcreteMotor;      // Invokes the set clause
```
```

Another approach to dependency injection is to use a *factory method* (which I discuss earlier in this chapter, in the section “As a method return type,” and illustrate in the section “Hiding Behind an Interface”):

```
```java
IPropulsion _propel = CreatePropulsion();    // A factory method
```
```