
## Configuring the Service

Microsoft .NET Framework provides a configuration editor tool, Microsoft Service Configuration Editor, to configure a service. To open Microsoft Service Configuration Editor, select Start→All Programs→Microsoft Visual Studio 2010→Microsoft Windows SDK Tools→Service Configuration Editor. Microsoft Service Configuration Editor appears, as shown in Figure 19.10:

![](img/e073a4882197be4ab61103cbe0bcb394_1014_0.png)

Figure 19.10: Showing Microsoft Service Configuration Editor

Now, select File→Open→Config File and locate the configuration file of your WCF service, such as web.config or app.config, to open it. Microsoft Service Configuration Editor displays the configuration details for the WCF service stored in the configuration file, as shown in Figure 19.11:

![](img/e073a4882197be4ab61103cbe0bcb394_1014_1.png)

Figure 19.11: Showing the Configuration Details of the MyFirstWCFService WCF Service

To configure a WCF service, you need to specify service bindings, endpoints, and service behavior.

### Specifying Service Bindings

You can specify bindings in a configuration file of your service by using Microsoft Service Configuration Editor. Let’s perform the following steps to specify bindings in the web.config file of a WCF service:

- 1. Right-click the Bindings folder in the Configuration pane and select the New Binding Configuration option, as shown in Figure 19.12:

![](img/e073a4882197be4ab61103cbe0bcb394_1015_0.png)

Figure 19.12: Showing the New Binding Configuration Option

The Create a New Binding dialog box opens, which prompts you to select a binding type from a list of binding types. In our case, we are creating a custom binding.

- 2. Select the customBinding option in the Create a New Binding dialog box, as shown in Figure 19.13:

![](img/e073a4882197be4ab61103cbe0bcb394_1015_1.png)

Figure 19.13: Showing the Create a New Binding Dialog Box

Now, a new customBinding pane appears in Microsoft Service Configuration Editor, which consists of various configuration options. The customBinding pane contains the Binding element extension position section that enables you to add, remove, and re-order the elements for the customBinding binding. By default, this section contains textMessageEncoding and httpTransport as Stack Elements (binding elements).

- 3. Remove the textMessageEncoding binding element and add the binaryMessageEncoding binding element in the Binding node of Microsoft Service Configuration Editor.

- 4. Add a reliableSession binding element at the top position under the Stack Element field. The order of the binding elements is important because it depicts the position of the binding elements in the channel stack.

- 5. Set the name of the reliableSession binding to NetHttpBinding, as shown in Figure 19.14:

![](img/e073a4882197be4ab61103cbe0bcb394_1016_0.png)

After configuring the custom binding, you need to specify the endpoints to use this custom binding.

### Specifying Endpoints

To specify the endpoints in the configuration file of your service, perform the following steps:

- 1. Right-click the Services folder and select the New Service option from the context menu, as shown in Figure 19.15:

![](img/e073a4882197be4ab61103cbe0bcb394_1016_1.png)

- 2. Change the name of the newly added service to Service.

- 3. Right-click the Endpoints folder and select the New Service Endpoint option from the context menu, as shown in Figure 19.16:

![](img/e073a4882197be4ab61103cbe0bcb394_1016_2.png)

- 4. Enter the name of the endpoint as HttpBinding, address as http://localhost:1982/MyFirstWCFService/Service.svc, binding as customBinding, binding configuration as NetHttpBinding, and contract as IService, in the respective fields, as shown in Figure 19.17:

![](img/e073a4882197be4ab61103cbe0bcb394_1017_0.png)

An endpoint is added in the Endpoints node of Microsoft Service Configuration Editor.

> **NOTE**
> You can also specify multiple endpoints for your service.

Now, let’s discuss about specifying the service behavior.

### Specifying the Service Behavior

Perform the following steps to specify the service behavior in the configuration file of your WCF service:

- 1. Expand the Advanced folder in the Configuration pane.
- 2. Right-click the Service Behaviors folder and select the New Service Behavior Configuration option from the context menu.
- 3. Change the name of the service behavior to MyServiceBehavior in the Service Behaviors node.
- 4. Add serviceMetadata, serviceDebug, and serviceThrottling in the Behavior element extension position section, as shown in Figure 19.18:

![](img/e073a4882197be4ab61103cbe0bcb394_1017_1.png)

![](img/e073a4882197be4ab61103cbe0bcb394_1019_0.png)

Figure 19.20: Adding a WCF Service to the SelfHostedService Application

- 3. Select the WCF Service template, specify an appropriate name for it, and click the Add button. In this case, the WCF service is named as UpperCaseService (Figure 19.20).

- 4. Open the IUpperCaseService.cs file, which is automatically created while creating the service, and add the following code snippet in the IUpperCaseService interface to declare the service contract:

```
[OperationContract]
string upperCase(string inputString);
```

- 5. Open the UpperCaseService.cs file and add the following code snippet to implement the service contract in the application:

```
public string upperCase(string inputString)
{
    string outputString = inputString.ToUpper();
    return outputString;
}
```

- 6. Open the code-behind file of Form1 (Form1.cs), and add the code, shown in Listing 19.7, to self-host the UpperCaseService service in Form1 of the SelfHostedService application:

**Listing 19.7:** Showing the Code for Hosting the UpperCaseService Service by Using the ServiceHost Class

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.ServiceModel;

namespace SelfHostedService
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        //Declaring an object of the ServiceHost class
        ServiceHost myServiceHost;

        private void Form1_Load(object sender, EventArgs e)
        {
            myServiceHost = new ServiceHost(typeof(UpperCaseService));
            button2.Enabled = false;
        }

        private void button1_Click(object sender, EventArgs e)
        {
            //Opening the ServiceHost object to listen to messages
            myServiceHost.Open();
            label1.Text = "The UpperCaseService service is now ";
            label2.Text = "Open";
            button2.Enabled = true;
            button1.Enabled = false;
        }

        private void button2_Click(object sender, EventArgs e)
        {
            //Close the ServiceHost object
            myServiceHost.Close();
            label1.Text = "The UpperCaseService service is now ";
            label2.Text = "Closed";
            button1.Enabled = true;
            button2.Enabled = false;
        }
    }
}
```

In Listing 19.7, an object (myServiceHost) of the ServiceHost class is created and then initialized at the loading time of Form1. The type of the WCF service (UpperCaseService) that you want to self-host is stored in the myServiceHost object. To use the ServiceHost class, you need to ensure that the System.ServiceModel namespace is added in the Form1.cs file.

On the button1_Click event, the myServiceHost object is opened to start hosting the UpperCaseService service by using the Open() method. Similarly, on the button2_Click event, the Close() method of the myServiceHost object is used to stop hosting the UpperCaseService service.

- 7. Press the F5 key to run the application. The output of the application appears, as shown in Figure 19.21:

![](img/e073a4882197be4ab61103cbe0bcb394_1020_0.png)

Figure 19.21: Showing the Output of the SelfHostedService Application

To allow the UpperCaseService service to be hosted in the SelfHostedService application, you need to click the Open Service button. The ServiceHost object is now open and the UpperCaseService service is hosted. The output after opening the service appears, as shown in Figure 19.22:

![](img/e073a4882197be4ab61103cbe0bcb394_1020_1.png)

Figure 19.22: Showing the Output when the Service is Hosted

- 8. Click the Close Service button; the ServiceHost object closes and stops the self-hosting of the service. The output after closing the service is shown in Figure 19.23:
