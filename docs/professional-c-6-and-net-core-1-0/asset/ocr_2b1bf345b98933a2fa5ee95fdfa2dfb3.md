```
<! &emsp14;&mdash; To avoid disclosing metadata information,
    set the value below to false and remove the metadata endpoint above
    before deployment &emsp14;&mdash; >
    <serviceMetadata httpGetEnabled="True"/>
    </behavior>
    </serviceBehaviors>
    </behaviors>
    </system.serviceModel>
</configuration>
```

Similar to the Add service reference from Visual Studio, the `Svcutil` utility needs metadata to create the proxy class. The `Svcutil` utility can create a proxy from the MEX metadata endpoint, the metadata of the assembly, or WSDL and XSD documentation:

```
svcutil http://localhost:8080/RoomReservation?wsdl /language:C#
/out:proxy.cs
svcutil CourseRegistration.dll
svcutil CourseRegistration.wsdl CourseRegistration.xsd
```

After the proxy class is generated, it just needs to be instantiated from the client code, the methods need to be called, and finally the `Close` method must be invoked:

```
var client = new RoomServiceClient();
client.RegisterForCourse(roomReservation);
client.Close();
```

# Sharing Types

The generated proxy class derives from the base class `ClientBase<TChannel>` that wraps the `ChannelFactory<TChannel>` class. Instead of using a generated proxy class, you can use the `ChannelFactory<TChannel>` class directly. The constructor requires the binding and endpoint address; next, you can create the channel and invoke methods as defined by the service contract. Finally, the factory must be closed:

```
var binding = new WsHttpBinding();
var address = new
EndpointAddress("http://localhost:8080/RoomService");

var factory = new ChannelFactory<IStateService>(binding,
address);

IRoomService channel = factory.CreateChannel();
channel.ReserveRoom(roomReservation);

// etc.
factory.Close();
```

The `ChannelFactory<TChannel>` class has several properties and methods, as shown in the following table.