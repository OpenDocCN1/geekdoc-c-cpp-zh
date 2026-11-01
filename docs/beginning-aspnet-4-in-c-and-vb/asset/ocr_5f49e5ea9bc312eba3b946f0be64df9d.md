To use a simple HTTP GET request to receive the reservations, the method GetRoomReservation needs a WebGet attribute to map the method parameters to the input from the GET request. In the following code, a UriTemplate is defined that requires Reservations to be added to the base address followed by From and To parameters. The From and To parameters in turn are mapped to the fromDate and toDate variables.

```
```csharp
[WebGet(UriTemplate="Reservations?From={fromDate}&To={toDate}")]
public RoomReservation[] GetRoomReservations(DateTime fromDate, DateTime toDate)
{
    var data = new RoomReservationData();
    return data.GetReservations(fromDate, toDate);
}
```
```

*code snippet RoomReservationService/RoomReservationService.cs*

Now the service can be invoked with a simple request as shown. All the reservations for the specified time frame are returned.

`http://localhost:8000/RoomReservation/Reservations?From=2010/1/16&To=2010/8/1`

# CLIENTS

A client application needs a proxy to access a service. There are three ways to create a proxy for the client:

+   - Visual Studio Add Service Reference — This utility creates a proxy class from the metadata of the service.
+   - ServiceModel Metadata Utility tool (Svcutil.exe) — You can create a proxy class with the Svcutil utility. This utility reads metadata from the service to create the proxy class.
+   - ChannelFactory class — This class is used by the proxy generated from Svcutil; however, it can also be used to create a proxy programmatically.

Adding a service reference from Visual Studio requires accessing a WSDL document. The WSDL document is created by a MEX endpoint that needs to be configured with the service. With the following configuration, the endpoint with the relative address mex uses the mexHttpBinding and implements the contract IMetadataExchange. To access the metadata with an HTTP GET request, the behaviorConfiguration MexServiceBehavior is configured.

```
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service behaviorConfiguration="MexServiceBehavior" name="Wrox.ProCSharp.WCF.RoomReservationService">
        <endpoint address="Test" binding="wsHttpBinding" contract="Wrox.ProCSharp.WCF.IRoomService" />
        <endpoint address="mex" binding="mexHttpBinding" contract="IMetadataExchange" />
        <host>
          <baseAddresses>
            <add baseAddress="http://localhost:8732/Design_Time_Addresses/RoomReservationService/" />
          </baseAddresses>
        </host>
      </service>
    </services>
    <behaviors>
      <serviceBehaviors>
        <behavior name="MexServiceBehavior">
        <!-- To avoid disclosing metadata information,
```
```