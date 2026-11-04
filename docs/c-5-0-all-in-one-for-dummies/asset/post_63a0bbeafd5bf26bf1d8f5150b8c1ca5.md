
## Getting to Know WCF

First there was DCOM. Then there was .NET Remoting.

The path to a distributed computing platform for Microsoft has been a long one. Distributed computing is a hard problem to solve — nothing bad on the Microsoft developers for continuing to hone their platform.

Anyway, there is SOAP, there are Microsoft binary formats, people are creating custom HTTP contexts — the distributed computing platform is a mess. Something needed to happen to enable you to all take your existing code and make it available across the enterprise.

The designers of WCF (largely Doug Purdy, Don Box, and crew) had two diverse issues. On one hand was ASMX, providing SOAP web service access to business logic. On the other hand was .NET Remoting, providing Microsoft a custom, black box format for the transmission of information between components via known network protocols.

In Chapter 2, I discuss ASMX and its limitations. Taking a deeper look at Remoting makes the case for a comprehensive platform even more clear (see Figure 3-1).

![](img/80ff26f06fc9ab951e1cd4257b867366_791_0.png)

If each of two systems, say a Client System and a Server System, had a similarly configured Remoting system, then they could communicate. The problem, of course, is that it was never, ever configured correctly (or so it seemed). One side of the equation or the other will make some change, and the whole system will come to a crashing halt.

Clearly, there has to be some product that brings the various formats of remoting access together under one umbrella — something that would accept one block of logic and provide multiple service types.

Eventually, WCF was that solution. Starting as an add-on to .NET 2.0, WCF effectively enabled developers to make specific endpoints for a generic connector.

Let's be clear about the problem we were trying to solve. Figure 3-2 shows the original problem illustrated by David Chappell for Microsoft back in 2007.

A car dealership is trying to build a new reservation application (similar to the conference management application of SHARP). The business logic needs to be both accessible to outside applications and provide a quality binary transport format for the internal communication.

WCF is the answer. It uses configuration to provide various endpoints to consuming applications, from SOAP to REST to binary associations that resemble DCOM. It doesn't require configuration on both ends of the pipe, only on the server side. If the server serves it, the client can consume it.

![](img/80ff26f06fc9ab951e1cd4257b867366_792_0.png)

Figure 3-2:
The original problem to be solved.

## Creating a WCF Service

As with so much in working with the .NET Framework, creating a WCF service isn't so much about the code as it is about the configuration. The SHARP project starts out a lot like the ASMX service.

To get started building out the SHARP service in WCF, follow these steps:

- 1. Open Visual Studio and click New Project.
- 2. Select the WCF Service Application in the WCF folder of the tree view.
- 3. Set up the project, as shown in Figure 3-3.
- 4. Click OK.

![](img/80ff26f06fc9ab951e1cd4257b867366_793_0.png)

Figure 3-3:
Starting the
new WCF
Service.

## Breaking it down

Look at the template code for a bit. It's nothing like the ASMX code because, remember, WCF is different. You can get it to do more or less the same thing as ASMX, but it isn't the same technology. Here's what the WCF code looks like:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.ServiceModel.Web;
using System.Text;

namespace SharpWcf
{
    // NOTE: You can use the "Rename" command on the "Refactor" menu to change
    // the class name "Service1" in code, svc and config file together.
    // NOTE: In order to launch WCF Test Client for testing this service, please
    // select Service1.svc or Service1.svc.cs at the Solution Explorer and start
    // debugging.

    public class Service1 : IService
    {
        public string GetData(int value)
        {
            return string.Format("You entered: {0}", value);
        }

        public CompositeType GetDataUsingDataContract(CompositeType composite)
        {
            if (composite == null)
            {
                throw new ArgumentNullException("composite");
            }
            if (composite.BoolValue)
            {
                composite.StringValue += "Suffix";
            }
            return composite;
        }
    }
}
```

A few of things are of interest here:

- **There is no [WebMethod] decoration.** You don’t need it in WCF. The whole object is a service project.
- **The class implements a custom interface, IService.** We look at that in a second.
- **There are two sample methods.** The usual old Hello World style method GetData, and a more complex example called `GetDataUsingContract`.

The GetDataUsingContract method makes a lot more sense when you take a look at IService.cs:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.ServiceModel.Web;
using System.Text;

namespace SharpWcf
{
    // NOTE: You can use the "Rename" command on the "Refactor" menu to change
    // the interface name "IService1" in both code and config file together.
    [ServiceContract]
    public interface IService1
    {
        [OperationContract]
        string GetData(int value);

        [OperationContract]
        CompositeType GetDataUsingDataContract(CompositeType composite);
    } // TODO: Add your service operations here
}

// Use a data contract as illustrated in the sample below to add composite types to service operations.
[DataContract]
public class CompositeType
{
    bool boolValue = true;
    string stringValue = "Hello ";

    [DataMember]
    public bool BoolValue
    {
        get { return boolValue; }
        set { boolValue = value; }
    }

    [DataMember]
    public string StringValue
    {
        get { return stringValue; }
        set { stringValue = value; }
    }
}
```

Hey, lookie here! Decorations for the classes! And the mythical CompositeType! Don't let the name fool you — this code is just a class, like any other class. It is just like the List<T> of Conference types that you returned from the ASMX service. The Framework doesn't have a Conference class — you defined it in the entity Data Model.

Line 4 has a [ServiceContract] attribute that is similar to the [WebClass] of ASMX, and the [OperationContract] too, is similar to [WebMethod], at least in usage.

Then you have the DataContract. This allows you to decorate classes — even in your domain model — with attributes that define which classes and methods get to go out to the service if and when the class is ever called into service (so to speak).

## Making a registration service

To make a registration service, start with a service that returns the list of your conferences. Follow these steps:

- 1. **Create a new WCF Service project.**
  I called mine `SHARPService`.
- 2. **Add a Class called Conference.**
  This will be a hand-rolled class that won't be connected to a database for now, but will provide a good example of how to set up a `DataContract`. This listing is the code-behind of the service file.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Runtime.Serialization;

namespace SHARPSERVICE
{
    public class Conference : SHARPSERVICE.IConference
    {
        public int Id { get; set; }
        public string Title { get; set; }
        public string Description { get; set; }
        public int LocationId { get; set; }
    }
}
```

You want this to be your DataContract for the service. Based on what you see in the template, you should add a [DataContract] above the class and [DataMember] above the properties.

- 3. Right-click the class name and, from the context menu, choose Refactor→Extract Interface.
- 4. Select all the public members and keep the default names like the dialog box in Figure 3-4.

![](img/80ff26f06fc9ab951e1cd4257b867366_796_0.png)

Figure 3-4:
Extracting the interface for the Conference class.

- 5. Add the DataContract for the service:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Runtime.Serialization;

namespace SHARPSERVICE
{
    [DataContract]
}
```
