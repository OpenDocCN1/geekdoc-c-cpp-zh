For this reason (among others, such as access coordination to remote objects), the industry has moved on to more service-oriented styles of programming, as exemplified by technologies like web services. In such a setting, one makes calls to operations defined on a (stateless) web service “façade,” serializing objects or unique identifiers across. For example, paying our John person would be done by making some Pay(8491, 124.45m) call, where 8491 is John’s unique identifier. The use of (static) web service façade methods gives rise to a more chunky form of communication. Now the transparency is limited to the operations defined on a web service proxy object and doesn’t get entangled with whole object graphs.

# A MarshalByRefObject Calculator Add-In

To continue our exploration of cross-domain communication between objects, let’s fix our Calc type by making it marshal by ref. You should feel free to experiment with a serializable object, as well, as explained before. Here is the adapted code that makes our Calc type amenable for use across application domains:

```
using System;

public class Calc : MarshalByRefObject
{
    public int Add(int a, int b)
    {
        Console.WriteLine(AppDomain.CurrentDomain);
        return a + b;
    }
}
```

Using our existing hosting code shown before, we can now get the calculator to work without the exception displayed in Figure 25.41. The use of .NET Remoting becomes apparent if we hover over the calc object and see its type, which reflects the use of a transparent proxy. Figure 25.44 shows how the remote object’s type name is buried in a series of indirections put in place by the .NET Remoting infrastructure.

![](bbox=[0.05, 0.9, 0.85, 0.97])

FIGURE 25.44 Transparent proxy type introduced by .NET Remoting.

Because our calculator’s Add method prints the application domain in which it’s executing, we can see the call is taking place in the AddIn domain. Try executing the same host but