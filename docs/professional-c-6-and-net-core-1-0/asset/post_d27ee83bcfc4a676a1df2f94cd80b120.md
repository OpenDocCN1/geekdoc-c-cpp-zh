
![](img/3d365b72b289213a91ade7eb366b8f35_1698_0.png)

Figure 44.2

## WCF Service Host and WCF Test Client

The WCF Service Library project template creates an application configuration file named App.config that you need to adapt to the new class and interface names. The service element references the service type RoomReservationService, including the namespace; the contract interface needs to be defined with the endpoint element (configuration file RoomReservation/RoomReservationService/app.config):

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.web>
    <compilation debug="true" />
  </system.web>
  <system.serviceModel>
    <services>
      <service name="Wrox.ProCSharp.WCF.Service.RoomReservationService">
        <endpoint address="" binding="basicHttpBinding"
                  contract="Wrox.ProCSharp.WCF.Service.IRoomReservationService">
          <identity>
            <dns value="localhost" />
          </identity>
        </endpoint>
        <endpoint address="mex" binding="mexHttpBinding"
                  contract="IMetadataExchange" />
        <host>
          <baseAddresses>
            <add baseAddress="http://localhost:8733/Design_Time_Addresses/RoomReservationService/" />
          </baseAddresses>
        </host>
      </service>
    </services>
    <behaviors>
      <serviceBehaviors>
        <behavior>
          <serviceMetadata httpGetEnabled="True"
                           httpsGetEnabled="True"/>
          <serviceDebug includeExceptionDetailInFaults="False" />
        </behavior>
      </serviceBehaviors>
    </behaviors>
  </system.serviceModel>
</configuration>
```

> NOTE The service address http://localhost:8733/Design_Time_Addresses has an access control list (ACL) associated with it that enables the interactive user to create a listener port. By default, a nonadministrative user is not allowed to open ports in listening mode. You can view the ACLs with the command-line utility netsh http show urlacl and add new entries with netsh http add urlacl url=http://+:8080/MyURI user=someUser listen=yes

Starting this library from Visual Studio 2015 starts the WCF Service Host, which appears as an icon in the notification area of the taskbar. Clicking this icon opens the WCF Service Host window (see Figure 44.3), where you can see the status of the service. The project properties of a WCF library application include the tab WCF options, where you can select whether the WCF service host should be started when running a project from the same solution. By default, this option is turned on. Also, with the Debug configuration of the project properties, you can find the command-line argument /client:"WcfTestClient.exe" defined. With this option, the WCF Service host starts the WCF Test Client (see Figure 44.4), which you can use to test the application. When you double-click an operation, input fields appear on the right side of the application that you can fill to send data to the service. When you click the XML tab, you can see the SOAP messages that have been sent and received.

![](img/3d365b72b289213a91ade7eb366b8f35_1699_0.png)

Figure 44.3

![](img/3d365b72b289213a91ade7eb366b8f35_1700_0.png)

Figure 44.4

## Custom Service Host

WCF enables services to run in any host. You can create a Windows Presentation Foundation (WPF) application for peer-to-peer services. Or you can create a Windows service or host the service with Windows Activation Services (WAS) or Internet Information Services (IIS). A console application is also good to demonstrate a simple custom host.

With the service host, you must reference the library RoomReservationService in addition to the assembly System.ServiceModel. The service is started by instantiating and opening an object of type ServiceHost. This class is defined in the namespace System.ServiceModel. The RoomReservationService class that implements the service is defined in the constructor. Invoking the Open method starts the listener channel of the service—the service is ready to listen for requests. The Close method stops the channel. The code snippet also adds a behavior of type ServiceMetadataBehavior. This behavior is added to allow creating a client application by using WSDL (code file RoomReservation/RoomReservationHost/Program.cs):

```csharp
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
            try
            {
                s_ServiceHost = new ServiceHost(typeof(RoomReservationService),
                    new Uri("http://localhost:9000/RoomReservation"));
                s_ServiceHost.Description.Behaviors.Add(
                    new ServiceMetadataBehavior
                    {
                        HttpGetEnabled = true
                    });
                s_ServiceHost.Open();
            }
            catch (AddressAccessDeniedException)
            {
                WriteLine("either start Visual Studio in elevated admin mode or register the listener port with netsh.exe");
            }
        }

        internal static void StopService()
        {
            if (s_ServiceHost != null &&
                s_ServiceHost.State == CommunicationState.Opened)
            {
                s_ServiceHost.Close();
            }
        }

        static void Main()
        {
            StartService();

            WriteLine("Server is running. Press return to exit");
            ReadLine();

            StopService();
        }
    }
}
```

For the WCF configuration, you can copy the application configuration file created with the service library to the host application. You can edit this configuration file with the WCF Service Configuration Editor (see Figure 44.5).

![](img/3d365b72b289213a91ade7eb366b8f35_1702_0.png)

Figure 44.5

Instead of using the configuration file, you can configure everything programmatically and also use several defaults. The sample code for the host application doesn’t need any configuration file. The second parameter of the ServiceHost constructor defines a base address for the service. With the protocol of this base address, a default binding is defined. The default for the HTTP is the BasicHttpBinding.

Using the custom service host, you can deselect the WCF option to start the WCF Service Host in the project settings of the WCF library.

## WCF Client

For the client, WCF is flexible in what application type can be used. The client can be a simple console application. However, for reserving rooms, you create a simple WPF application with controls, as shown in Figure 44.6.

Room Reservation

|     |     |
|-----|-----|
| Room: | |
| Begin time: | |
| End time: | |
| Contact: | |
| Event: | |

Reserve Room

Figure 44.6

Because the service host is configured with the ServiceMetadataBehavior, it offers a MEX endpoint. After the service host is started, you can add a service reference from Visual Studio. After you add the service reference, the dialog shown in Figure 44.7 pops up. Enter the link to the service metadata with the URL http://localhost:9000/RoomReservation?wsdl, and set the namespace name to RoomReservationService. This defines the namespace of the generated proxy class.

Figure 44.7

Adding a service reference adds references to the assemblies System.Runtime.Serialization and System.ServiceModel, and it also adds a configuration file containing the binding information and the endpoint address to the service.

From the data contract, the class RoomReservation is generated as a partial class. This class contains all [DataMember] elements of the contract. The class RoomReservationServiceClient is the proxy for the client that contains methods that are defined by the operation contracts. Using this client, you can send a room reservation to the running service.

In the code file RoomReservation/RoomReservationClient/MainWindow.xaml.cs, the OnReserveRoom method is invoked with the Click event of the button. The ReserveRoomAsync is invoked with the service proxy. The reservation variable receives the data from the UI via data binding.

```csharp
public partial class MainWindow : Window
{
    private RoomReservation _reservation;

    public MainWindow()
    {
        InitializeComponent();
        _reservation = new RoomReservation
        {
            StartTime = DateTime.Now,
            EndTime = DateTime.Now.AddHours(1)
        };
        this.DataContext = _reservation;
    }
}
```
