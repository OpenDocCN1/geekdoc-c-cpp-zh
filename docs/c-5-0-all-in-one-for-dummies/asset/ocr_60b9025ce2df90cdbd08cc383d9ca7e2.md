![](bbox=[0.14, 0.17, 0.22, 0.32])

The preceding example only protects your user interface from experiencing a tie-up. You still have no real indication that the messages will ever be delivered, so you should never write software that depends on the delivery of the data from the service. It has to fail gracefully.

# Contract driven

In client-server development, an interface defines a contract of sorts between the domain model and the user interface. You can use that contract to drive development in the same way that you use a contract to drive a business deal. If you know what I require and I know what you require, we can quickly and easily make a deal.

A web service is required to have an interface that conforms to the Web Services Description Language (WSDL) standard. WSDL describes expected inputs and allowed outputs just as an interface would, creating a contract between the service provider and the client.

In .NET, your contract is created automatically from the code for the service. If you call a service in the browser (which isn't the way it's designed to be called — I tell you more about that topic later in this minibook) from the development machine, you see the test screen shown in Figure 1-1. Even though the browser gains some basic important information about the service, it isn't the contract. The contract is shown behind the Service Description link.

![](bbox=[0.28, 0.62, 0.9, 0.92])

Figure 1-1:
The default service overview.