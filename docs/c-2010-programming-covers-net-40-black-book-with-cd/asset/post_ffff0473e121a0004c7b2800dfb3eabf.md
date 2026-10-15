
through which remote messages flow. An object of the BinaryClientFormatterSinkProvider class represents a client formatter sink that provides necessary properties to serialize the message to the stream.

The class hierarchy of the BinaryClientFormatterSinkProvider class is shown as follows:

```
System.Object
System.Runtime.Remoting.Channels.BinaryClientFormatterSinkProvider
```

Table 35.15 shows the property provided by the BinaryClientFormatterSinkProvider class:

| Table 35.15: Noteworthy Property of the BinaryClientFormatterSinkProvider Class |
| Property | Description |
| includeVersions | Specifies whether the formatter will include versioning information. |

You can see the noteworthy public constructor of the BinaryClientFormatterSinkProvider class in Table 35.16:

| Table 35.16: Public Constructor of the BinaryClientFormatterSinkProvider Class |
| Constructor | Description |
| BinaryClientFormatterSinkProvider | Initializes a new instance of the BinaryClientFormatterSinkProvider class |

Table 35.17 shows the noteworthy public property of the BinaryClientFormatterSinkProvider class:

| Table 35.17: Public Property of the BinaryClientFormatterSinkProvider Class |
| Property | Description |
| Next | Obtains or sets the next IClientChannelSinkProvider in the sink provider chain |

The noteworthy public method of the BinaryClientFormatterSinkProvider class is shown in Table 35.18:

| Table 35.18: Noteworthy Public Method of the BinaryClientFormatterSinkProvider Class |
| Method | Description |
| CreateSink() | Creates a sink chain |

You can also use the BinaryServerFormatterSinkProvider class to provide the implementation for the server formatter channel sink provider that uses the BinaryFormatter class to serialize messages to the stream.

The class hierarchy of the BinaryServerFormatterSinkProvider class is shown as follows:

```
System.Object
System.Runtime.Remoting.Channels.BinaryServerFormatterSinkProvider
```

Table 35.19 shows the property provided by the BinaryServerFormatterSinkProvider class:

| Table 35.19: Noteworthy Property of the BinaryServerFormatterSinkProvider Class |
| Property | Description |
| includeVersions | Specifies whether the formatter will include versioning information. |

You can find the noteworthy public constructor of BinaryServerFormatterSinkProvider class in Table 35.20:

| Table 35.20: Noteworthy Public Constructor of the BinaryServerFormatterSinkProvider Class |
| Constructor | Description |
| BinaryServerFormatterSinkProvider | Initializes a new instance of the BinaryServerFormatterSinkProvider class |

## Chapter 35: .NET Remoting in C# 2010

The noteworthy public properties of the BinaryServerFormatterSinkProvider class are described in Table 35.21:

| Property | Description |
|----------|-------------|
| Next | Sets the next IServerChannelSinkProvider in the sink provider chain |
| TypeFilterLevel | Sets the level of automatic deserialization for .NET remoting |

Table 35.22 describes the noteworthy public methods of BinaryServerFormatterSinkProvider class:

| Method | Description |
|--------|-------------|
| CreateSink() | Creates a sink chain |
| GetChannelData() | Returns the channel data for the channel with which the current sink is associated |

The SOAPFormatter class converts an object's state into a SOAP format. SOAP is an XML-based protocol used to exchange information between applications. As some network transports do not allow you to send and receive binary data; therefore, they force applications to convert all binary data into an American Standard Code for Information Interchange (ASCII) text representation before sending it over a channel. In such situations, the SOAPFormatter class is used to send and receive the data. The SOAPFormatter class is defined in the System.Runtime.Serialization.Formatters.Soap namespace. The SOAPFormatter class is used by an object of the SoapClientFormatterSinkProvider class to serialize messages for the client channel through which remote messages flow. An object of the SoapClientFormatterSinkProvider class represents a client formatter sink that provides necessary properties to serialize the message to the stream.

The class hierarchy of the SoapClientFormatterSinkProvider class is shown as follows:

```
System.Object
System.Runtime.Remoting.Channels.SoapClientFormatterSinkProvider
```

| Property | Description |
|----------|-------------|
| includeVersions | Specifies whether the formatter will include versioning information |

| Constructor | Description |
|--------------|-------------|
| SoapClientFormatterSinkProvider | Initializes a new instance of the SoapClientFormatterSinkProvider class |

| Property | Description |
|----------|-------------|
| Next | Obtains or sets the next IClientChannelSinkProvider in the sink provider chain |

Real proxy – Creates the illusion that the actual object resides on a client when the client and server are in different application domains. The real proxy actually sends and receives the messages from a remote object. A real proxy is implemented by using the RealProxy class.
Let’s learn how to host a remote object in .NET.

## Hosting of Remote Objects

A remote object of server can be readily available to a client, when it is properly hosted by using a Windows service or a Component Object Model (COM)+ service. You can also host a remote object on IIS, in which a configuration file is created to host the remote object. To host remote objects in IIS, you need to create a virtual directory and copy the web.config file that contains all the remoting settings related to remotable objects in the virtual directory. After copying the web.config file, you need to place the executable or Dynamic Link Library (DLL) containing the remote object in the bin directory of IIS root. It is important to note that the IIS root name should be the same as the application name specified in the configuration files. The remoting configuration file is automatically loaded when the first message arrives in the application. In this way, .NET remoting objects can be exposed as Web services. A sample code of the web.config file is shown in the following code snippet:

```
<configuration>
  <system.runtime.remoting>
    <application>
      <service wellknown mode="Singleton" objectUri="HiServerApp.soap" type="SharedObject.SharedObject, SharedObject"/>
      <channels><channel ref="http">
        <serverProviders>
          <provider ref="soap" typeFilterLevel="full" />
          <provider ref="wsdl" remoteApplicationMetadataEnabled="true"/>
        </serverProviders>
      </channel></channels>
    </application>
  </system.runtime.remoting>
</configuration>
```

Let’s learn about the lease time of objects.

## Setting the Lease Time of an Object

When an object is published and has started interacting with external AppDomains, a decision has to be taken about the lease time of the remote object, which refers to the time after which the object would not be used by anyone. When the lease time of an object has reached, the object marked for deletion is destroyed by garbage collector. The concept of lease time applies to a Singleton or client activated object only. By default, the time of five minutes is specified to a client object. However, you can change this default time in the constructor of your remote object, as shown in the following code snippet:

```
public override object InitializeLifetimeService()
{
  ILease myLease = (ILease)base.InitializeLifetimeService();
  myLease.InitialLeaseTime = TimeSpan.FromMinutes(10);
  myLease.RenewOnCallTime = TimeSpan.FromMinutes(50);
  return myLease;
}
```

Let’s now move to the Immediate Solutions section of the chapter.

## Immediate Solutions

### Creating and Using Application Domains

A .NET application is loaded in an application domain, which is called the default application domain for that application. However, you can create additional application domains and use them in your applications. In this section, you learn to create and use application domains by creating two Windows Forms applications, named AppOne and AppTwo. The design and source code of these applications are available in the AppDomains folder on CD.

Perform the following steps to create and run the AppOne and AppTwo applications:

+   1. Create the AppOne application by designing Form1 with two button controls, whose text is set as Execute AppTwo and Access Object Created in the Default AppDomain.

+   2. Add a simple class, named AClassInAppOne, in the AppOne application. Listing 35.1 shows the source code of the AClassInAppOne class:

### Listing 35.1: Showing the Code of the AClassInAppOne Class in the AppOne Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace AppOne
{
    class AClassInAppOne
    {
        public AClassInAppOne(string Msg)
        {
            MessageBox.Show("Creating Instance with message = " +Msg+ " in AppDomain " + AppDomain.CurrentDomain.FriendlyName);
        }
        public void ASimpleMethod()
        {
            MessageBox.Show("Called In AppDomain " + AppDomain.CurrentDomain.FriendlyName);
        }
    }
}
```

+   3. Add the code given in Listing 35.2 in the Form1.cs file of the AppOne application:

### Listing 35.2: Showing the Code of the Form1.cs File of the AppOne Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace AppOne
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        private void button1_Click(object sender, EventArgs e)
        {
            AppDomain SecondAppDomain = AppDomain.CreateDomain("Second AppDomain");
```
