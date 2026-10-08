# Extending the Editor with the Managed Extensibility Framework

The key technology enabling the creation of custom editor components new in .NET 4 is the Managed Extensibility Framework (MEF). The MEF is not a part of Visual Studio 2010. However, Visual Studio 2010 is one of the first Microsoft products that uses the MEF. The following discussion does not go into detail about the MEF, but provides a very brief overview to help you understand what it is and how it works.

Simply said, the MEF as a technology is intended to enable greater reuse of applications and components by turning today's statically compiled applications into dynamically composed ones.
Why is this dynamic composition so important? If you create applications from smaller independent parts, you can architect the application so that responsibilities are better defined. According to these responsibilities, you can separately test your parts, find bugs, and correct them. It is easier to handle these small parts individually than all of the pieces together, and (as you can imagine) it is easier to maintain them. However, the big issue is how to roll these individual parts to a whole application.

This is what the MEF does — parts declare their intention to work with other pieces, and the MEF pulls all these parts together to form the application.

In the case of extending the Visual Studio 2010, the host is Visual Studio, and the custom editor components are the parts to be composed dynamically with the editor within the IDE. The intention of parts for cooperation can be one of the following:

+   * A part can offer some functionality to be used by the host.
* A part wants to use some services implemented by the host.
* A combination of these two.

The MEF uses .NET attributes for cooperation. These attributes can be found in the System.ComponentModel.Composition namespace.

# Using Export Attributes

The intention that a component offers a service to be consumed by other components is expressed with the Export attribute. For example, if you have an abstract service described with the IGreetings interface that contains a SayHello method, a custom part accessible from other MEF-components looks like this:

```
[Export(typeof(IGreetings))]
class SimpleGreeting : IGreetings
{
    public string SayHello()
    {
        return "Hello from Visual Studio 2010";
    }
}
```