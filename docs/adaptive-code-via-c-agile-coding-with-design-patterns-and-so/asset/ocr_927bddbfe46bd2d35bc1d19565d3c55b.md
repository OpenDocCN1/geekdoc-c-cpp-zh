# FIGURE 5-5 The Composite pattern closely resembles the Decorator pattern.

The Composite pattern’s purpose is to allow you to treat many instances of an interface as if they were just one instance. Therefore, clients can accept just one instance of an interface, but they can be implicitly provided with many instances, without requiring the client to change. Listing 5-14 shows a composite decorator in practice.

# LISTING 5-14 The composite implementation of an interface.

Click here to view code image

```
public interface IComponent
{
    void Something();
}
//...
public class Leaf : IComponent
{
    public void Something()
    {
    }
}
//...
```