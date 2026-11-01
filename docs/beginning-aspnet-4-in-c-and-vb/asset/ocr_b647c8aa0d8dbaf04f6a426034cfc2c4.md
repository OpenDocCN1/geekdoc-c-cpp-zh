The following sections discuss the details and different options of WCF.

# CONTRACTS

A contract defines what functionality a service offers and what functionality can be used by the client. The contract can be completely independent of the implementation of the service.

The contracts defined by WCF can be grouped into three different contract types: data, service, and message. The contracts can be specified by using .NET attributes:

+   - **Data contract** — The data contract defines the data received by and returned from the service. The classes used for sending and receiving messages have data contract attributes associated with them.
+   - **Service contract** — The service contract is used to define the WSDL that describes the service. This contract is defined with interfaces or classes.
+   - **Message contract** — If complete control over the SOAP message is needed, a message contract can specify what data should go into the SOAP header and what belongs in the SOAP body.

The following sections explore these contract types further and discuss versioning issues that should be thought about when defining the contracts.

# Data Contract

With the data contract, CLR types are mapped to XML schemas. The data contract is different from other .NET serialization mechanisms: with runtime serialization, all fields are serialized (including private fields); with XML serialization, only the public fields and properties are serialized. The data contract requires explicit marking of the fields that should be serialized with the DataMember attribute. This attribute can be used regardless of whether the field is private or public, or if it is applied to a property.

```
[DataContract(Namespace="http://www.thinktecture.com/SampleServices/2010")]
public class RoomReservation
{
    [DataMember] public string Room { get; set; }
    [DataMember] public DateTime StartDate { get; set; }
    [DataMember] public DateTime EndDate { get; set; }
    [DataMember] public string ContactName { get; set; }
    [DataMember] public string EventName { get; set; }
}
```

To platform-independent, and provide the option to change data with new versions without breaking older clients and services, using data contracts is the best way to define which data should be sent. However, you can also use XML serialization and runtime serialization. XML serialization is the mechanism used by ASP.NET Web services, .NET Remoting uses runtime serialization.

With the attribute DataMember, you can specify the properties described in the following table.

| DATAMEMBER PROPERTY | DESCRIPTION |
|---|---|
| Name | By default, the serialized element has the same name as the field or property where the [DataMember] attribute is applied. You can change the name with the Name property. |
| Order | The Order property defines the serialization order of the data members. |
| IsRequired | With the IsRequired property, you can specify that the element must be received with serialization. This property can be used for versioning. If you add members to an existing contract, the contract is not broken because, by default, the fields are optional (IsRequired=false). You can break an existing contract by setting IsRequired to true. |
| EmitDefaultValue | The property EmitDefaultValue defines whether the member should be serialized if it has the default value. If EmitDefaultValue is set to true, the member is not serialized if it has the default value for the type. |