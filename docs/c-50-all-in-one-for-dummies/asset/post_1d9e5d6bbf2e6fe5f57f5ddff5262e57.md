
## Getting to Know WCF

First there was DCOM. Then there was .NET Remoting.

The path to a distributed computing platform for Microsoft has been a long one. Distributed computing is a hard problem to solve — nothing bad on the Microsoft developers for continuing to hone their platform.

Anyway, there is SOAP, there are Microsoft binary formats, people are creating custom HTTP requests — the distributed computing platform is a mess. Something needed to have to enable you to take all your existing code and make it available across the enterprise.

The designers of WCF (largely Doug Purdy, Don Box, and crew) had two diverse ones. On one hand was ASMX, providing web service access to business logic. On the other hand was .NET Remoting, providing Microsoft a custom, black box format for the transmission of information between components via known network protocols.

In Chapter 2, I discuss ASMX and its limitations. Taking a deeper look at Remoting makes the case for a comprehensive platform even more clear (see Figure 3-1).

![](img/6df7bb88e9302e98442acc219cfbd7fc_791_0.png)

Each of two systems, say a Client System and a Server System, had a similarly configured Remoting system, then they could communicate. The problem, of course, is that it was never, ever configured correctly (or so seemed). One of the equation or the other will make some change, and the whole system will come to a crashing fault.

Clearly, there has to be some product that brings the various formats of remote access together under one umbrella — something that would accept one block of logic and provide multiple service types.

Eventually, WCF was that solution. Starting as an add-on to .NET 2.0, WCF effectively enabled developers to make specific endpoints for a generic connector.

## Creating a WCF Service

Let's be clear about the problem we were trying to solve. Figure 3-2 shows the original problem illustrated by David Chappel for Microsoft back in 2007.

A dealership is trying to build a new reservation application (similar to the conference management application of SHARP). The business logic needs to be both accessible to outside applications and provide a quality binary transport format for the internal communication.

WCF is the answer. It uses configuration to provide various endpoints to consuming applications, from SOAP to REST to binary associations that resemble DCOM. It doesn't require configuration on both ends of the pipe, only on the server side. If the server serves it, the client can consume it.

![](img/6df7bb88e9302e98442acc219cfbd7fc_792_0.png)

## Creating a WCF Service

As with so much in working with the .NET Framework, creating a WCF service isn't so much about the code as it is about the configuration. SHARP project starts out a lot like the ASMX service.

## Creating a WCF Service

To get started building out the SHARP service in WCF, follow these steps:

- 1. Open Visual Studio and click New Project.
- 2. Select the WCF Service Application in the WCF folder of the tree.
- 3. Set up the project, as shown in Figure 3-3.
- 4. Click OK.

![](img/6df7bb88e9302e98442acc219cfbd7fc_793_0.png)

Figure 3-3:
Starting the new WCF Service.

## Breaking down

Look the template code for a bit. It's not like the ASMX code, remember, WCF is different. You can get it to do more or the same thing as ASMX, but it isn't the same technology. Here's what the WCF code looks like:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.ServiceModel.Web;
using System.Text;
```

```
namespace SharpWcf
{
// NOTE: You can use the "Rename" command on the "Refactor" to change
the class name "ServiceModel" in code, svc and config file together.
// NOTE: In order to launch WCF Test Client for testing this service,
select Service.svc or Service.svc.cs at the Solution Explorer and start
debugging.
```

```
public class Service1 : IService
{
    public string GetData(int value)
    {
        return string.Format("You entered: (0)", value);
    }

    public CompositeType GetDataUsingDataContract(CompositeType composite)
    {
        if (composite == null)
        {
            throw new ArgumentNullException("composite");
        }
        if (composite.BoolValue)
        {
            composite.Value += "Suffix";
        }
        return composite;
    }
}
```

There are a few things of interest here:

- There is no [WebMethod] decoration. You don't need it in WCF. The whole project is a service project.
- The class implements a custom interface, IService. We look at in a second.
- There are two sample methods. The old Hello World method GetData, and a more complex example called GetDataUsingContract.

The GetDataUsingContract method makes a lot more sense when you take a look at IService.cs.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.ServiceModel.Web;
using System.Text;
```

```
namespace SharpWcf
{
[ServiceContract]
public interface IService1
{
    [OperationContract]
    string GetData(int value);

    [OperationContract]
    CompositeType GetDataUsingDataContract(CompositeType composite);
}
```

## Creating a WCF Service

[DataContract]
public class CompositeType
{
    [DataMember]
    public bool BoolValue { get; set; }
    [DataMember]
    public string Value { get; set; }
}

[DataContract]
public class Conference
{
    [DataMember]
    public int Id { get; set; }
    [DataMember]
    public string Title { get; set; }
    [DataMember]
    public string Description { get; set; }
    [DataMember]
    public int LocationId { get; set; }
}

## Making a registration service

To make a registration service, start with a service that returns the list of conferences. Follow these steps:

- 1. Create a new WCF project. I called mine SHARPService.
- 2. Add a Class called Conference. This will be a hand-rolled class that won't connected to a data-base for now, but will provide a good example of how to set up a DataContract. This listing is the code-behind of the service.
- 3. Right-click the class name, and from the menu, choose Refactor: Extract Interface.
- 4. Select all the public members and keep the default names the dialog box in Figure 3-4.

