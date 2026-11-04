There isn't a binding in the WCF Configuration tool for the ReST binding. however, so we have to do it another way. Just follow these steps:

+   1. **Open the Web.Config for the service.**
+   There should be binding information in there from the SOAP service we built in Chapter 3. Leave that there.
+   
+   2. **Add the bold listing for the custom POX binding under the ServiceModel section.**
+   It is the first bold code in Listing 4-1.
+   
+   3. **Add the Service information into the Service section. It is the second bold code in Listing 4-1.**

# Listing 4-1: The ReST Service Implementation

```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.0">
      <assemblies>
        <add assembly="System.Data.Entity, Version=4.0.0.0, Culture=neutral, Publ
iKeyToken=b77a5c561934e089" />
      </assemblies>
    </compilation>
  </system.web>
  <system.serviceModel>
    <bindings>
      <customBinding>
        <binding name="poxBinding">
          <textMessageEncoding messageVersion="None" />
          <httpTransport />
        </binding>
      </customBinding>
    </bindings>
    <services>
      <service name="SHARPSERVICE.Registration">
        <clear />
        <endpoint address="http://localhost" binding="basicHttpBinding" name="SharpHttp" contract="SHARPSERVICE.Iregistration" listenUriMode="Explicit">
          <identity>
            <certificateReference storeName="My" storeLocation="LocalMachine" x509FindType="FindBySubjectDistinguishedName" />
          </identity>
        </endpoint>
        <endpoint address="http://localhost" binding="wsDualHttpBinding" bindingConfiguration="" name="SharpDual" contract="SHARPSERVICE.Iregistration" />
      </service>
      <service name="SHARPSERVICE.Registration">
        <host>
          <baseAddresses>
            <add baseAddress="http://localhost" />
          </baseAddresses>
        </host>
```