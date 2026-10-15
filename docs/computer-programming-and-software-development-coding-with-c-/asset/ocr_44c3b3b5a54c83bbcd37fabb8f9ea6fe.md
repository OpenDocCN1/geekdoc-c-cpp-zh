```
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```

Most of these interfaces are very simple. As you can see here, for example, the ICloneable. The interface just defines a method Clone that we need to implement. When then somewhere else a clone of an object implementing this interface is invoked, our code will be invoked. Let's return to Visual Studio and implement one of these commonly used interfaces, IComparable. Then I'll show you what extra behavior we are getting by implementing this interface. I have changed the Employee class again slightly.