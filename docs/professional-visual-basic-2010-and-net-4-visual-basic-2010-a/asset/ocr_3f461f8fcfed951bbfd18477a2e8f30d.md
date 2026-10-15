to Configure Your Service Reference. This key dialog enables you to edit these values to reflect your service’s specific needs.

The second important part of this configuration document is the <client> element. This element contains a child element called <endpoint> that defines the where and how of the service consumption process.

The <endpoint> element provides the address of the service — and it specifies which binding of the available WCF bindings should be used. In this case, the wsHttpBinding is the required binding. Although you are using an established binding from the WCF framework, from the client side you can customize how this binding behaves. As noted, the settings that define the behavior of the binding are specified using the bindingConfiguration attribute of the <endpoint> element. In this case, the value provided to the bindingConfiguration attribute is WSHttpBinding_ICalculator, which is a reference to the <binding> element contained within the <wsHttpBinding> element:

```
<binding name="WSHttpBinding_ICalculator" closeTimeout="00:01:00"
openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00"
bypassProxyOnLocal="false" transactionFlow="false"
hostNameComparisonMode="StrongWildcard"
maxBufferPoolSize="524288" maxReceivedMessageSize="65536"
messageEncoding="Text" textEncoding="utf-8" useDefaultWebProxy="true"
allowCookies="false">
<readerQuotas maxDepth="32" maxStringContentLength="8192" maxArrayLength="16384"
maxBytesPerRead="4096" maxNameTableCharCount="16384" />
<reliableSession ordered="true" inactivityTimeout="00:10:00" enabled="false" />
<security mode="Message">
<transport clientCredentialType="Windows" proxyCredentialType="None"
realm="" />
<message clientCredentialType="Windows" negotiateServiceCredential="true"
algorithmSuite="Default" />
</security>
</binding>
```

Note one important distinction here. If instead of using the built-in Visual Studio test engine to test your service declaration, you bound to the custom client, you would find that this configuration file would be subtly different. Instead of having a wsHttpBinding, you would have a netTCP binding. This binding would have different setting defaults and, more important, indicate a different transport protocol for your requests. If you play with these two different bindings, you’ll find that the binary format used by netTCP responds much more quickly than the wsHttpBinding that Visual Studio has generated for you.

As demonstrated, the Visual Studio 2010 capabilities for WCF make the consumption of these services fairly trivial. The next step is to code the Windows Forms project to test the consumption of the service interface.

# Writing the Consumption Code

The code to consume the interface is quite minimal. End users will merely select the radio button of the operation they want to perform. The default radio button selected is Add. The user places a number in each of the two text boxes provided and clicks the Calculate button to call the service to perform the designated operation on the provided numbers.

To accomplish this, add two text boxes, four radio buttons, one button, and one label to your form. The display (for labeling the controls) should look similar to what is shown in Figure 13-11. Next, you want to create two event handlers; the first is on Form Load to pre-populate the text boxes with default numbers (to speed testing), and the second is an event handler for the button you’ve labeled Calculate.

Clicking the Calculate button will create an instance of the service and then open a connection and make the appropriate call. In a production environment, you might keep a static instance of the service available in your application so you could create it once instead of for each event. Similarly, you’ll want to follow the best practice mentioned earlier of assigning the URI at runtime based on an application setting.