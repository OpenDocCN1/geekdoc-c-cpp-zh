# Interfaces

Let's use the previous example of **Male** and **Female** classes. Fast forward 20 years from now, and we discover aliens on Mars. They are surprisingly similar to us, making them human, but they are neither male nor female. We now have a new type, **Alien**, which inherits from the abstract class **Human**.

Now think of interfaces as verbs. Which verb can be applied to my classes in general? All humans need to learn new things and can be taught, so now we can create an interface called **ITeachable**. We will implement the **ITeachable** interface on the **Human** abstract class, because all humans are teachable. The aliens, however, are slightly more advanced than **Male** or **Female**, and can rearrange their molecules into different structures, making aliens able to shape-shift. Therefore, we can create an interface called **IShapeShiftable**, which only applies to **Alien**.

Creating the interface is much like the abstract class. It also needs to contain a contract class, and the interface and contract class both need to point to each other via their attributes.

```
```csharp
using System.Diagnostics.Contracts;

[ContractClass(typeof(IShapeShiftableContract))]
public interface IShapeShiftable
{
    void Man(int shapeDuration);
    void Woman(int shapeDuration);
    void InanimateObject(int shapeDuration);
}

[ContractClassFor(typeof(IShapeShiftable))]
abstract class IShapeShiftableContract : IShapeShiftable
{
    void IShapeShiftable.InanimateObject(int shapeDuration)
    {
        Contract.Requires(shapeDuration <= 12);
    }

    void IShapeShiftable.Man(int shapeDuration)
    {
        Contract.Requires(shapeDuration <= 4);
    }

    void IShapeShiftable.Woman(int shapeDuration)
    {
        Contract.Requires(shapeDuration <= 4);
    }
}
```
```

Code Listing 53: Interface Implementing Code Contract Class