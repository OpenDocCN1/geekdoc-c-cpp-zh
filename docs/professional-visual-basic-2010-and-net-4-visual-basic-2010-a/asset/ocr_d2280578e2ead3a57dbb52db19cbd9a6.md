A couple of things are going on in this file. First, in order to gain access to work with any of the WCF framework pieces, you need a reference to the `System.ServiceModel` and the `System.ServiceModel.Description` namespaces in the file. The `System.ServiceModel` gives you access to defining things such as the endpoints that you need to create, while the `System.ServiceModel.Description` namespace reference gives you access to defining things such as the WSDL file.

Remember that creating endpoints uses the ABC model (address, binding, and contract). The address part here is `net.tcp://localhost:8080/Calculator`. The binding is a TCP binding — `NetTcpBinding` — while the contract part is the `ICalculator` interface.

Many different bindings are available to you when coding WCF services. Here, this example makes use of the NetTcpBinding. The full list of available bindings is as follows:

+   - System.ServiceModel.BasicHttpBinding
+   - System.ServiceModel.Channels.CustomBinding
+   - System.ServiceModel.MsmqBindingBase
+   - System.ServiceModel.NetNamedPipeBinding
+   - System.ServiceModel.NetPeerTcpBinding
+   - System.ServiceModel.NetTcpBinding
+   - System.ServiceModel.WebHttpBinding
+   - System.ServiceModel.WSDualHttpBinding
+   - System.ServiceModel.WSHttpBindingBase

Clearly, several bindings are available. In the preceding example, the `NetTcpBinding` class is the transport pipe being used. This means that the service being built will be delivered over TCP. At this point your development environment should look similar to what is shown in Figure 13-5. However, before running the new console, let’s look at the various commands it will use to host your custom service.

![](bbox=[0.095, 0.531, 0.75, 0.923])

# FIGURE 13-5