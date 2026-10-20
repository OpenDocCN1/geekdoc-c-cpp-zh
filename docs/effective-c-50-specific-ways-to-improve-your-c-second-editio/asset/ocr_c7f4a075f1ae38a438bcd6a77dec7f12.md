tion. You do not fill out one product line, fax it, add your address, fax again, add your credit card number, and fax again.

This illustrates the common pitfalls of a poorly defined service interface. Whether you use a Web service, .NET Remoting, or Azure-based programming, you must remember that the most expensive part of the operation comes when you transfer objects between distant machines. You must stop creating remote APIs that are simply a repackaging of the same local interfaces that you use. It works, but it reeks of inefficiency. It’s using the phone call metaphor to process your catalog request via fax. Your application waits for the network each time you make a round-trip to pass a new piece of information through the pipe. The more granular the API is, the higher percentage of time your application spends waiting for data to return from the server.

Instead, create Web-based interfaces based on serializing documents or sets of objects between client and server. Your remote communications should work like the order form you fax to the catalog company: The client machine should be capable of working for extended periods of time without contacting the server. Then, when all the information to complete the transaction is filled in, the client can send the entire document to the server. The server’s responses work the same way: When information gets sent from the server to the client, the client receives all the information necessary to complete all the tasks at hand.

Sticking with the customer order metaphor, we’ll design a customer order-processing system that consists of a central server and desktop clients accessing information via Web services. One class in the system is the customer class. If you ignore the transport issues, the customer class might look something like this, which allows client code to retrieve or modify the name, shipping address, and account information:

```
public class Customer
{
    public Customer()
    {
    }

    // Properties to access and modify customer fields:
    public string Name { get; set; }

    public Address ShippingAddr { get; set; }
```