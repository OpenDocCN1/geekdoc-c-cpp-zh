![](bbox=[0.05, 0.05, 0.95, 0.32])

# Figure 44.4

# Custom Service Host

WCF enables services to run in any host. You can create a Windows Presentation Foundation (WPF) application for peer-to-peer services. Or you can create a Windows service or host the service with Windows Activation Services (WAS) or Internet Information Services (IIS). A console application is also good to demonstrate a simple custom host.

With the service host, you must reference the library RoomReservationService in addition to the assembly System.ServiceModel. The service is started by instantiating and opening an object of type ServiceHost. This class is defined in the namespace System.ServiceModel. The RoomReservationService class that implements the service is defined in the constructor. Invoking the Open method starts the listener channel of the service—the service is ready to listen for requests. The Close method stops the channel. The code snippet also adds a behavior of type ServiceMetadataBehavior. This behavior is added to allow creating a client application by using WSDL (code file RoomReservation/RoomReservationHost/Program.cs):

```
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Wrox.ProCSharp.WCF.Service;
using static System.Console;

namespace Wrox.ProCSharp.WCF.Host
{
    class Program
    {
        internal static ServiceHost s_ServiceHost = null;

        internal static void StartService()
        {
        }
    }
}
```