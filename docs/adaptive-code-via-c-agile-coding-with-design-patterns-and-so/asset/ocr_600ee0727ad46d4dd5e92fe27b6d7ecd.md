In the CompositeComponent class, there are methods for adding and removing other instances of the IComponent. These methods do not form part of the interface and are for clients of the CompositeComponent class, directly. Whichever factory method or class is tasked with creating instances of the CompositeComponent class will also have to create the decorated instances and pass them into the Add method; otherwise, the clients of the IComponent would have to change in order to cope with compositions.

Whenever the Something method is called by the IComponent clients, the list of composed instances is enumerated, and their respective Something is called. This is how you reroute the call to a single instance of IComponent—of type CompositeComponent—to many other types.

Each instance that you supply to the CompositeComponent class must implement the IComponent interface—and this is enforced by the compiler due to C#’s strong typing—but the instances need not all be of the same concrete type. Because of the advantages of polymorphism, you can treat all implementations of an interface as instances of that interface. In the example shown in Listing 5-15, the CompositeComponent instances provided are of different types, further enhancing this pattern’s utility.

# LISTING 5-15 Instances provided to the composite can be of different types.

Click here to view code image

```
public class SecondTypeOfLeaf : IComponent
{
    public void Something()
    {
    }
}
//...
public class AThirdLeafType : IComponent
{
    public void Something()
    {
    }
}
//...
public void AlternativeComposite()
{
    var composite = new CompositeComponent();
    composite.AddComponent(new Leaf());
    composite.AddComponent(new SecondTypeOfLeaf());
    composite.AddComponent(new AThirdLeafType());

    component = composite;
    composite.Something();
```