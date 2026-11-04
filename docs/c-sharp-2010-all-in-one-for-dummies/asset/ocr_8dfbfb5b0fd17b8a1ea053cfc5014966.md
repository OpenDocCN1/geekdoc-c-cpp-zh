```
AddStuffReference.ServiceISoapClient client = new AddStuffReference.ServiceISoapClient();
client.AddStuffCompleted += new EventHandler(client_AddStuffCompleted);
client.AddStuffAsync("This is the stuff");
}

//This method is called when the response comes back.
//No timers or anything. .NET handles it for you.
void proxy_AddStuffCompleted(object sender, AddStuffReference.ServiceISoapClient.AddStuffCompletedEventArgs e)
{
    bool result = e.Result.ToString();
}
```

![](bbox=[0.1, 0.52, 0.22, 0.68])

The example above only protects your user interface from experiencing a tie-up. You still have no real indication that the messages will ever be delivered, so you should never write software that depends on the delivery of the data from the service. It has to fail gracefully.

# Contract driven

In client-server development, an interface defines a contract of sorts between the domain model and the user interface. That contract can be used to drive development in the same way as a contract is used to drive a business deal. If you know what I require and I know what you require, we can quickly and easily make a deal.

A Web service is required to have an interface that conforms to the Web Services Description Language (WSDL) standard. WSDL describes expected inputs and allowed outputs just as an interface would, creating a contract between the service provider and the client.

In .NET, your contract is created automatically from the code for the service. If you call a service in the browser (which isn't the way it's designed to be called — I tell you more about that topic later in this minibook) from the development machine, you see the test screen shown in Figure 1-1. Even though the browser gains some basic important information about the service, it isn't the contract. The contract is shown behind the Service Description link.

Clicking the Service Description link appends the text ?WSDL to the URI, and the Web browser shows the contract. This contract is used by the client system to determine exactly which information the service wants and how it will respond to input. Though the WSDL is displayed in a browser, as shown in Figure 1-2, the interesting part is the XML that's behind the screen.