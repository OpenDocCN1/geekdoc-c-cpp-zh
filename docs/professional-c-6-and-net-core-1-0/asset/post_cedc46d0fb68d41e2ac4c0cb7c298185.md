
```csharp
private async void OnReserveRoom(object sender,
RoutedEventArgs e)
{
    var client = new RoomServiceClient();
    bool reserved = await client.ReserveRoomAsync(reservation);
    client.Close();
    if (reserved)
    {
        MessageBox.Show("reservation ok");
    }
}
}
```

With the settings of the RoomReservation solution, you can configure multiple startup projects, which should be RoomReservationClient and RoomReservationHost in this case. By running both the service and the client, you can add room reservations to the database.

## Diagnostics

When running a client and service application, it can be helpful to know what’s happening behind the scenes. For this, WCF makes use of a trace source that just needs to be configured. You can configure tracing using the Service Configuration Editor, selecting Diagnostics, and enabling Tracing and Message Logging. Setting the trace level of the trace sources to Verbose produces detailed information. This configuration change adds trace sources and listeners to the application configuration file as shown here:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <connectionStrings>
        <add
            name="RoomReservation"
            providerName="System.Data.SqlClient"
            connectionString="Server=(localdb)\mssqllocaldb;Database=RoomReservation;
            Trusted_Connection=true;MultipleActiveResultSets=True" />
    </connectionStrings>

    <system.diagnostics>
        <sources>
            <source name="System.ServiceModel.MessageLogging"
                switchValue="Verbose,ActivityTracing">
                <listeners>
                    <add type="System.Diagnostics.DefaultTraceListener"
name="Default">
                        <filter type="" />
                    </add>
                    <add name="ServiceModelMessageLoggingListener">
                        <filter type="" />
                    </add>
                </listeners>
            </source>
            <source propagateActivity="true"
name="System.ServiceModel"
                switchValue="Warning,ActivityTracing">
                <listeners>
                    <add type="System.Diagnostics.DefaultTraceListener"
name="Default">
                        <filter type="" />
                    </add>
                    <add name="ServiceModelTraceListener">
                        <filter type="" />
                    </add>
                </listeners>
            </source>
        </sources>
        <sharedListeners>
            <add initializeData="c:\logs\wcf\roomreservation\roomreservationhost\app_messages.svclog"
                type="System.Diagnostics.XmlWriterTraceListener, System,
                Version=4.0.0.0, Culture=neutral,
                PublicKeyToken=b77a5c561934e089"
                name="ServiceModelMessageLoggingListener"
                traceOutputOptions="DateTime, Timestamp, ProcessId,
ThreadId">
                <filter type="" />
            </add>
            <add initializeData="c:\logs\wcf\roomreservation\roomreservationhost\app_tracelog.svclog"
                type="System.Diagnostics.XmlWriterTraceListener, System,
                Version=4.0.0.0, Culture=neutral,
                PublicKeyToken=b77a5c561934e089"
                name="ServiceModelTraceListener"
                traceOutputOptions="DateTime, Timestamp, ProcessId,
ThreadId">
                <filter type="" />
            </add>
        </sharedListeners>
    </system.diagnostics>
    <startup>
        <supportedRuntime version="v4.0"
sku=".NETFramework,Version=v4.6" />
    </startup>
    <system.serviceModel>
        <diagnostics>
            <messageLogging logEntireMessage="true"
logMalformedMessages="true"
                logMessagesAtTransportLevel="true" />
            <endToEndTracing propagateActivity="true"
activityTracing="true"
                messageFlowTracing="true" />
        </diagnostics>
    </system.serviceModel>
</configuration>
```

> NOTE The implementation of the WCF classes uses the trace sources named System.ServiceModel and System.ServiceModel.MessageLogging for writing trace messages. You can read more about tracing and configuring trace sources and listeners in Chapter 20, “Diagnostics and Application Insights.”

When you start the application, the trace files soon get large with verbose trace settings. To analyze the information from the XML log file, the .NET SDK includes the Service Trace Viewer tool, svctraceviewer.exe. Figure 44.8 shows the client application with

![](img/3d365b72b289213a91ade7eb366b8f35_1708_0.png)

Figure 44.9

The following sections discuss the details and different options of WCF.

## Sharing Contract Assemblies with the Client

With the previous WPF client application, a proxy class was created using the metadata, adding a service reference with Visual Studio. You can also create a client by using the shared contract assembly as is shown now. Using the contract interface, the ChannelFactory<TChannel> class is used to instantiate the channel to connect to the service.

The constructor of the class ChannelFactory<TChannel> accepts the binding configuration and endpoint address. The binding must be compatible with the binding defined with the service host, and the address defined with the EndpointAddress class references the URI of the running service. The CreateChannel method creates a channel to connect to the service. Then you can invoke methods of the service (code file RoomReservation/RoomReservationClientSharedAssembly/MainWindow.xaml.cs):

```csharp
using System;
using System.ServiceModel;
using System.Windows;
using Wrox.ProCSharp.WCF.Contracts;

namespace RoomReservationClientSharedAssembly
{
    public partial class MainWindow : Window
    {
        private RoomReservation _roomReservation;

        public MainWindow()
        {
            InitializeComponent();
            _roomReservation = new RoomReservation
            {
                StartTime = DateTime.Now,
                EndTime = DateTime.Now.AddHours(1)
            };
            this.DataContext = _roomReservation;
        }

        private void OnReserveRoom(object sender, RoutedEventArgs e)
        {
            var binding = new BasicHttpBinding();
            var address = new EndpointAddress(
                "http://localhost:9000/RoomReservation");
            var factory = new ChannelFactory<IRoomService>(binding, address);
            IRoomService channel = factory.CreateChannel();
            if (channel.ReserveRoom(_roomReservation))
            {
                MessageBox.Show("success");
            }
        }
    }
}
```

## Contracts

A contract defines what functionality a service offers and what functionality can be used by the client. The contract can be completely independent of the implementation of the service.

The contracts defined by WCF can be grouped into four different contract types: Data, Service, Message, and Fault. The contracts can be specified by using .NET attributes:

- **Data contract**—the data contract defines the data received by and returned from the service. The classes used for sending and receiving messages have data contract attributes associated with them.
- **Service contract**—the service contract is used to define the WSDL that describes the service. This contract is defined with interfaces or classes.
- **Operation contract**—the operation contract defines the operation of the service and is defined within the service contract.
- **Message contract**—If you need complete control over the SOAP message, a message contract can specify what data should go into the SOAP header and what belongs in the SOAP body.
- **Fault contract**—the fault contract defines the error messages that are sent to the client.

The following sections explore these contract types further and discuss versioning issues that you should think about when defining the contracts.

## Data Contract

With the data contract, CLR types are mapped to XML schemas. The data contract is different from other .NET serialization mechanisms: with runtime serialization, all fields are serialized (including private fields); with XML serialization, only the public fields and properties are serialized. The data contract requires explicit marking of the fields that should be serialized with the DataMember attribute. This attribute can be used regardless of whether the field is private or public, or if it is applied to a property.

```csharp
[DataContract(Namespace="http://www.cninnovation.com/Services/20:

public class RoomReservation
{
    [DataMember] public string Room { get; set; }
    [DataMember] public DateTime StartTime { get; set; }
    [DataMember] public DateTime EndTime { get; set; }
    [DataMember] public string Contact { get; set; }
    [DataMember] public string Text { get; set; }
}
```

To be platform-independent and provide the option to change data with new versions without breaking older clients and services, using data contracts is the best way to define which data should be sent. However, you can also use XML serialization and runtime serialization. XML serialization is the mechanism used by ASP.NET web services; .NET Remoting uses runtime serialization.

With the attribute DataMember, you can specify the properties described in the following table.
