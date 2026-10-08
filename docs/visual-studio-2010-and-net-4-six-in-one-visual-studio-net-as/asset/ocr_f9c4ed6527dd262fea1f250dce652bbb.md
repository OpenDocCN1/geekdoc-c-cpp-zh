In this example, the EmployeeClass is defined as a data contract, and each of the members within the class is offered as a DataMember. If you have a property that is calculated or otherwise shouldn't be passed across the communication wire, you can omit the DataMember attribute.

# Specifying the Binding Information

Now that you have created the service, data contract, and the service implementation, you must specify the binding information for the service to make it accessible by services or clients. For a WCF service to be accessed by the clients, the service must expose at least one endpoint. An endpoint denotes the address, binding, and contract information for the service.

To specify the binding information for the service, open the App.Config file and insert the following code inside the <system.serviceModel> tags:

```
<system.serviceModel>
 <bindings>
  <basicHttpBinding>
    <binding name="BasicHttpBinding_EmployeeDataService">
      closeTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00"
      allowCookies="false" bypassProxyOnLocalAddress="false"
      hostNameComparisonMode="StrongWildcard"
      maxBufferSize="65536" maxBufferPoolSize="52428"
      maxReceivedMessageSize="65536"
      messageEncoding="Text" encoding="utf-8" transferMode="Buffered"
      useHttps="true"
      <readerQuota maxDepth="32" maxContentLength="8192" maxArrayLength="16384" />
      maxBytesPerReader="4096" maxNameTableCharCount="16384 />
      <security mode="None">
        <transport clientCredentialType="None" proxyCredentialType="None" />
        <message clientCredentialType="Username" algorithmSuite="Default" />
      </security>
    </binding>
  </basicHttpBinding>
 </bindings>
 <client>
  <endpoint address="http://myservice/DataService.svc" binding="basicHttpBinding" bindingConfiguration="BasicHttpBinding_EmployeeDataService" contract="IEmployeeDataService" name="BasicHttpBinding_EmployeeDataService" />
 </client>
</system.serviceModel>
```

This creates a basicHttpBinding for the example service specifying additional properties on the binding (such as the openTimeout, receiveTimeout, send timeout, bufferSize, and maximum message size). Additional configuration on the binding specifies that no security is used for the transport. The endpoint is defined with an address that specifies