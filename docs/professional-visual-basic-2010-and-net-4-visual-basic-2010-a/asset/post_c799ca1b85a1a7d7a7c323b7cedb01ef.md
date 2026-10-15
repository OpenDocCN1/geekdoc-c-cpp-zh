
## Configuration File Changes

Another addition to your project is the `app.config` file. After the service reference is made, the `app.config` file contains several new configuration settings. These configuration settings were automatically added by the Visual Studio WCF extensions. The new `app.config` file is presented in the following code block:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0,Profile=Client" />
  </startup>
  <system.serviceModel>
    <bindings>
      <wsHttpBinding>
        <binding name="WSHttpBinding_ICalculator" closeTimeout="00:01:00" openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00" bypassProxyOnLocal="false" transactionFlow="false" hostNameComparisonMode="StrongWildcard" maxBufferPoolSize="524288" maxReceivedMessageSize="65536" messageEncoding="Text" textEncoding="utf-8" useDefaultWebProxy="true" allowCookies="false">
          <readerQuotas maxDepth="32" maxStringContentLength="8192" maxArrayLength="16384" maxBytesPerRead="4096" maxNameTableCharCount="16384" />
          <reliableSession ordered="true" inactivityTimeout="00:10:00" enabled="false" />
          <security mode="Message">
            <transport clientCredentialType="Windows" proxyCredentialType="None" realm="" />
            <message clientCredentialType="Windows" negotiateServiceCredential="true" algorithmSuite="Default" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    <client>
      <endpoint address="http://localhost:8732/Design_Time_Addresses/ProVB_WCFCalculatorLibrary/Service1/" binding="wsHttpBinding" bindingConfiguration="WSHttpBinding_ICalculator" contract="CalculatorService.ICalculator" name="WSHttpBinding_ICalculator">
        <identity>
          <dns value="localhost" />
        </identity>
      </endpoint>
    </client>
  </system.serviceModel>
</configuration>
```

Code snippet from app.config

There are two important parts to this file. First, the information in the `wsHttpBinding` section is important because this defines behaviors such as the timeouts and the maximum amount of data that can be placed in a message. It is not uncommon for these defaults to prevent people from successfully sending messages and cause great confusion. Note that if you right-click on your service reference, another context menu option is Configure Service Reference. This key dialog enables you to edit these values to reflect your service’s specific needs.

The second important part of this configuration document is the `<client>` element. This element contains a child element called `<endpoint>` that defines the where and how of the service consumption process.

The `<endpoint>` element provides the address of the service — and it specifies which binding of the available WCF bindings should be used. In this case, the `wsHttpBinding` is the required binding. Although you are using an established binding from the WCF framework, from the client side you can customize how this binding behaves. As noted, the settings that define the behavior of the binding are specified using the `bindingConfiguration` attribute of the `<endpoint>` element. In this case, the value provided to the `bindingConfiguration` attribute is `WSHttpBinding_ICalculator`, which is a reference to the `<binding>` element contained within the `<wsHttpBinding>` element:

```xml
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

Note one important distinction here. If instead of using the built-in Visual Studio test engine to test your service declaration, you bound to the custom client, you would find that this configuration file would be subtly different. Instead of having a `wsHttpBinding`, you would have a `netTCP` binding. This binding would have different setting defaults and, more important, indicate a different transport protocol for your requests. If you play with these two different bindings, you’ll find that the binary format used by `netTCP` responds much more quickly than the `wsHttpBinding` that Visual Studio has generated for you.

As demonstrated, the Visual Studio 2010 capabilities for WCF make the consumption of these services fairly trivial. The next step is to code the Windows Forms project to test the consumption of the service interface.

## Writing the Consumption Code

The code to consume the interface is quite minimal. End users will merely select the radio button of the operation they want to perform. The default radio button selected is Add. The user places a number in each of the two text boxes provided and clicks the Calculate button to call the service to perform the designated operation on the provided numbers.

To accomplish this, add two text boxes, four radio buttons, one button, and one label to your form. The display (for labeling the controls) should look similar to what is shown in Figure 13-11. Next, you want to create two event handlers; the first is on Form Load to pre-populate the text boxes with default numbers (to speed testing), and the second is an event handler for the button you’ve labeled Calculate.

Clicking the Calculate button will create an instance of the service and then open a connection and make the appropriate call. In a production environment, you might keep a static instance of the service available in your application so you could create it once instead of for each event. Similarly, you’ll want to follow the best practice mentioned earlier of assigning the URI at runtime based on an application setting.

![](img/d99870e80390742f93963da7be0b2e61_541_0.png)

**FIGURE 13-11**

The code for the form is as follows:

```vb
Public Class Form1
    Private Sub Form1_Load(ByVal sender As System.Object,
        ByVal e As System.EventArgs) Handles MyBase.Load
        TextBox1.Text = "21"
        TextBox2.Text = "21"
    End Sub

    Private Sub Button1_Click(ByVal sender As System.Object,
        ByVal e As System.EventArgs) Handles Button1.Click
        Dim result As Integer
        Dim ws As New CalculatorService.CalculatorClient()
        ws.Open()
        If RadioButton1.Checked = True Then
            result = ws.Add(Integer.Parse(TextBox1.Text), Integer.Parse(TextBox2.Text))
        ElseIf RadioButton2.Checked = True Then
            result = ws.Subtract(Integer.Parse(TextBox1.Text),
                Integer.Parse(TextBox2.Text))
        ElseIf RadioButton3.Checked = True Then
            result = ws.Multiply(Integer.Parse(TextBox1.Text),
                Integer.Parse(TextBox2.Text))
        ElseIf RadioButton4.Checked = True Then
            result = ws.Divide(Integer.Parse(TextBox1.Text),
                Integer.Parse(TextBox2.Text))
        End If
        ws.Close()
        Label1.Text = result.ToString()
    End Sub

End Class
```

Code snippet from Form1.vb

This is quite similar to the steps taken when working with Web references from the XML Web Services world. First is an instantiation of the proxy class, as shown with the creation of the `ws` object:

```vb
Dim ws As New CalculatorService.CalculatorClient()
```

Working with the `ws` object now, the IntelliSense options provide you with the appropriate Add, Subtract, Multiply, and Divide methods. Running this application provides results similar to those presented in Figure 13-12.

In this case, the Add method is invoked from the service when the form’s Calculate button is pressed.

Another best practice is to get a tool such as Fiddler2 to track communication with your service. (www.fiddler2.com/fiddler2/) This free tool enables you to view messages sent across an HTTP/HTTPS.

Note that while this tool will work if you’ve used Visual Studio to configure your testing to be transported via HTTP, if you’ve relied on the custom client, you’ll find that the requests are instead sent as binary data over TCP and are not available to Fiddler2.

Using a binding to the custom client means the requests and responses are sent over TCP as binary, dramatically decreasing the size of the payload for large messages. This is something that .NET Remoting was used for prior to the release of the WCF framework.

This concludes the short tutorial demonstrating how to build a single service that can support two different endpoints. Visual Studio 2010 can generate one such endpoint, which is based on the same XML and open standards as a traditional Web service. The other you built manually into your command-line application to support the TCP protocol and binary data transfer. Depending on how you map that service to your client, you can consume the service as either an XML-based data transfer or a binary data transfer that can map directly into your .NET Windows Forms application.

![](img/d99870e80390742f93963da7be0b2e61_542_0.png)

**FIGURE 13-12**

## WORKING WITH DATA CONTRACTS

In the preceding sample WCF service, the data contract depended upon simple types or primitive data types. A .NET type of Integer was exposed, which in turn was mapped to an XSD type of int. You might not have noticed the input and output types actually defined in the WSDL document that was provided via the WCF-generated one, but they are there. These types are exposed through an imported .xsd document (a dynamic document). This bit of the WSDL document is presented here:

```xml
<wsdl:types>
  <xsd:schema targetNamespace="http://tempuri.org/Imports">
    <xsd:import schemaLocation="http://localhost:8000/calculator?xsd=xsd0" namespace="http://tempuri.org/" />
    <xsd:import schemaLocation="http://localhost:8000/calculator?xsd=xsd1" namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
  </xsd:schema>
</wsdl:types>
```

Typing in the XSD location of `http://localhost:8000/calculator?xsd=xsd0` gives you the input and output parameters of the service. For instance, looking at the definition of the Add method, you will see the following bit of XML:

```xml
<xs:element name="Add">
  <xs:complexType>
    <xs:sequence>
      <xs:element minOccurs="0" name="a" type="xs:int" />
      <xs:element minOccurs="0" name="b" type="xs:int" />
    </xs:sequence>
  </xs:complexType>
</xs:element>
<xs:element name="AddResponse">
  <xs:complexType>
```
