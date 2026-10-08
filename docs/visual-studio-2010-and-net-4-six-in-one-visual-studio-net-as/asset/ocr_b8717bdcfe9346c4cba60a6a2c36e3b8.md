serviceHost.Close();

}

}

You can refer to the examples in Chapter 9 of this book for an example of the long-hand setup that is needed to configure WCF prior to the 4.0 release.

Client consumption configuration has also been greatly simplified, with the following items being the only necessary configuration:

```
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <behaviors>
      <serviceBehaviors>
        <behavior>
          <serviceMetadata httpGetEnabled="true"/>
        </behavior>
      </serviceBehaviors>
    </behaviors>
  </system.serviceModel>
</configuration>
```
```

This configures everything using the default configuration, which uses a BasicHttpBinding. If you need to do any further configuration, or use a more secure binding protocol (such as wsHttpBinding), you only need to add an additional protocolMapping code to your configuration, similar to the following:

```
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <behaviors>
      <serviceBehaviors>
        <behavior>
          <serviceMetadata httpGetEnabled="true"/>
        </behavior>
      </serviceBehaviors>
    </behaviors>
    <protocolMapping>
      <add binding="wsHttpBinding" scheme="http"/>
    </protocolMapping>
  </system.serviceModel>
</configuration>
```
```

# # Standard Endpoints

Standard endpoints are items provided by the .NET framework that can be used to more quickly configure standard endpoints for common application functions. Table 13-1 shows the standard endpoints for WCF 4.0.