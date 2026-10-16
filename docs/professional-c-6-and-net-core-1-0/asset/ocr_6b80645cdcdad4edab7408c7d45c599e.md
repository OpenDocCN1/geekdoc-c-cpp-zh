```
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
```

# Contracts

A contract defines what functionality a service offers and what functionality can be used by the client. The contract can be completely independent of the implementation of the service.

The contracts defined by WCF can be grouped into four different contract types: Data, Service, Message, and Fault. The contracts can be specified by using .NET attributes:

+   - **Data contract**—The data contract defines the data received by and returned from the service. The classes used for sending and receiving messages have data contract attributes associated with them.
+   - **Service contract**—The service contract is used to define the WSDL that describes the service. This contract is defined with interfaces or classes.
+   - **Operation contract**—The operation contract defines the operation of the service and is defined within the service contract.
+   - **Message contract**—If you need complete control over the SOAP message, a message contract can specify what data should go into the SOAP header and what belongs in the SOAP body.
+   - **Fault contract**—The fault contract defines the error messages that are sent to the client.

The following sections explore these contract types further and discuss versioning issues that you should think about when defining the contracts.