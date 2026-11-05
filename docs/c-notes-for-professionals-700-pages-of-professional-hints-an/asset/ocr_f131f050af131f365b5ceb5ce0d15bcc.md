# Chapter 164: Windows Communication Foundation

Windows Communication Foundation (WCF) is a framework for building service-oriented applications. Using WCF, you can send data as asynchronous messages from one service endpoint to another. A service endpoint can be part of a continuously available service hosted by IIS, or it can be a service hosted in an application. The messages can be as simple as a single character or word sent as XML, or as complex as a stream of binary data.

# Section 164.1: Getting started sample

The service describes the operations it performs in a service contract that it exposes publicly as metadata.

```
```csharp
// Define a service contract.
[ServiceContract(Namespace="http://StackOverflow.ServiceModel.Samples")]
public interface ICalculator
{
    [OperationContract]
    double Add(double n1, double n2);
}
```
```

The service implementation calculates and returns the appropriate result, as shown in the following example code.

```
```csharp
// Service class that implements the service contract.
public class CalculatorService : ICalculator
{
    public double Add(double n1, double n2)
    {
        return n1 + n2;
    }
}
```
```

The service exposes an endpoint for communicating with the service, defined using a configuration file (Web.config), as shown in the following sample configuration.

```
```xml
<services>
    <service
        name="StackOverflow.ServiceModel.Samples.CalculatorService"
        behaviorConfiguration="CalculatorServiceBehavior">
        <!-- ICalculator is exposed at the base address provided by host: http://localhost/servicemodelsamples/service.svc. -->
        <endpoint address=""
            binding="wsHttpBinding"
            contract="StackOverflow.ServiceModel.Samples.ICalculator" />
        ...
    </service>
</services>
```
```

The framework does not expose metadata by default. As such, the service turns on the ServiceMetadataBehavior and exposes a metadata exchange (MEX) endpoint at http://localhost/servicemodelsamples/service.svc/mex. The following configuration demonstrates this.

```
```xml
<system.serviceModel>
    <services>
        <service
            name="StackOverflow.ServiceModel.Samples.CalculatorService"
```
```