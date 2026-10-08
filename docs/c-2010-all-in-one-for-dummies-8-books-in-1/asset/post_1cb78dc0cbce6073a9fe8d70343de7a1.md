
# Building Service-Oriented Applications 727

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_752_0.png)

**Figure 1-4:** Separating the layers.

Because the services use a common format — usually XML over HTTP — you can relatively easily install parts of the application on their own machines to isolate them by functionality. Because the functionality of the deleted part is called via a service, you can scale the application horizontally.

- **Reusability:** Every organization has a list of its participants — clients, users, voters, cooks, or mailing list subscribers, for example. Regardless of the type of participant, all the people on the list have first and last names and identifying characteristics.

It seems like nearly every application written today has a table of People. Savvy programmers use slick tricks to keep these tables in sync or to share information, for example, but only one way exists to share the People table — by using a data silo, as shown in Figure 1-5.

A data silo works this way:

- 1. A database on some server contains all participants' demographic information.
- 2. The data silo is surrounded by a service layer containing all allowed operations.
- 3. The service layer is consumed by all other applications in the system, as shown in Figure 1-5.

This set of steps shows you the concept of reuse. It isn't about bits of code (no matter what you might hear) — it's about *data*. Services help to provide access to the data silo.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_753_0.png)

Figure 1-5: A data silo.

# Providing XML Web Services

A common use of services is to give other programmers public access to your information by using an open API that can be consumed anywhere. You might recall the WSDL file, described in the earlier section “Contract driven”—it can make your cool function or valuable data available to anyone who needs it.

In the demographic silo example, described in the earlier section “Building Service-Oriented Applications,” if you have a valuable mailing list and want to give your customers access to it, you can send them the list. If you do, however, they can use it forever. Instead, suppose that you could bill your customers every time they use the list. If you provide Web services to implemented functions on the list, you can then track actual usage of the list.

You can see this concept, known as provision past the boundary, everywhere. Take Twitter, for example. Rather than making users to go the Web page to search through billions of messages, Twitter provides a WSDL contract that gives developers the ability to search in their own applications.

Web services can be controlled like any other Web application. The field-level or operation-level security that used to be handled at the RDBMS level can now be built into a semipublic API.

# Building Three Sample Apps

You can build services in C# in a few ways, as described in the next three chapters. This section's heading isn't exactly right, however: I show how to build the same app in three different ways. The app, the SHARP conference system (or a simple version of it), was built using these formats:

- **ASMX:** This first version is in the venerable ASMX format: ASP.NET Web services. Though this format has been largely superseded by WCF, it's still available. I cover it in this chapter and the next because it's a viable solution for certain situations.
- **WCF:** Windows Communications Foundation (WCF), the most important service platform, is given enough screen time to get you started. The topic is broad, and you can find lots of references to other resources.
- **REST:** Representational State Transfer (REST), the oldest service on the planet, has a new life, thanks to AJAX. REST isn't a first-class citizen in the .NET world, but it's important.

The entire process uses a single data model, shown in Figure 1-6, and provides allowed operations to it.

| Conferences | | Sessions | Column-Name | Data Type | Allow Null |
| :--- | :--- | :--- | :--- | :--- |
| Id | | Id | int | [x] |
| Description | | varchar(1024) | [x] |
| LocationId | | text | [x] |
| | | NumberExpected | int | [x] |
| | | Speaker | int | [x] |
| | | StartTime | date | [x] |
| | | EndTime | datetime | [x] |
| | | ConferenceId | int | [x] |
| Locations | | | | | |
| Id | | | | | |
| PlaceName | | | | |

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_754_0.png)

| Attending | People |
| :--- | :--- |
| Id | Id |
| PlaceName | FirstName |
| SessionId | LastName |
| | EmailAddress |

The idea is to provide a service model similar to the heating system platform described earlier in this chapter, except using a real, stateful, data-driven application.

Finally, I show you how to solve three different problems. Then you can shoot for three different outcomes. Otherwise, what fun would it be?

# Chapter 2: Building Web Services with ASMX

In This Chapter

- Getting acquainted with ASMX
- Creating ASMX
- Building ASMX

In this chapter, we'll get acquainted with ASMX. We'll learn how to create and build ASMX services. We'll also learn how to use ASMX in a real-world application.

In the next chapter, we'll look at WCF. We'll learn how to create and build WCF services. We'll also learn how to use WCF in a real-world application.

In the final chapter, we'll look at REST. We'll learn how to create and build REST services. We'll also learn how to use REST in a real-world application.

# Building Web Services with ASMX

ASMX is the simplest way to build web services in ASP.NET. It's easy to learn, but it's not the most powerful. In this chapter, we'll learn how to build a simple ASMX service.

To create an ASMX service, you need to create a class and add the [WebMethod] attribute to your methods.

```csharp
[WebServiceService]
public class HelloWorldService : WebService
{
    [WebMethod]
    public string HelloWorld(string name)
    {
        return "Hello " + name;
    }
}
```

This is a very simple ASMX service. It has one method, HelloWorld, which takes a string as an input and returns a string.

In the next example, we'll build a more complex ASMX service. This service will have multiple methods, and it will use data types.

```csharp
[WebServiceService]
public class CalculatorService : WebService
{
    [WebMethod]
    public int Add(int a, int b)
    {
        return a + b;
    }

    [WebMethod]
    public int Subtract(int a, int b)
    {
        return a - b;
    }

    [WebMethod]
    public int Multiply(int a, int b)
    {
        return a * b;
    }

    [WebMethod]
    public int Divide(int a, int b)
    {
        if (b == 0)
        {
            throw new ArgumentException("Cannot divide by zero.");
        }
        return a / b;
    }
}
```

This is a more complex ASMX service. It has four methods, and it uses integer data types.

To use an ASMX service, you can use the Web Service Reference tool in Visual Studio.

```csharp
CalculatorService service = new CalculatorService();
int result = service.Add(5, 10);
Console.WriteLine(result);
```

This is how you use an ASMX service in your client code.

In the next example, we'll build an ASMX service that uses custom objects.

```csharp
[Serializable]
public class Person
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Email { get; set; }
}

[WebServiceService]
public class PersonService : WebService
{
    [WebMethod]
    public Person GetPerson(int id)
    {
        // In a real application, this would fetch the person from a database.
        return new Person
        {
            Id = id,
            FirstName = "John",
            LastName = "Doe",
            Email = "john.doe@example.com"
        };
    }
}
```

This is an ASMX service that uses custom objects. To use this service, you need to include the Person class in your client code.

```csharp
PersonService service = new PersonService();
Person person = service.GetPerson(1);
Console.WriteLine(person.FirstName + " " + person.LastName);
```

This is how you use an ASMX service that uses custom objects.

# Building Web Services with WCF

WCF is the modern way to build web services in .NET. It's more complex than ASMX, but it's also more powerful. In this chapter, we'll learn how to build a simple WCF service.

To build a WCF service, you first need to define an interface for your service.

```csharp
[ServiceContract]
public interface IHelloWorldService
{
    string HelloWorld(string name);
}
```

Then, you implement the interface in a class.

```csharp
public class HelloWorldService : IHelloWorldService
{
    public string HelloWorld(string name)
    {
        return "Hello " + name;
    }
}
```

Finally, you need to host the service. You can host it in IIS.

```xml
<services>
  <service name="HelloWorldService">
    <endpoint address=""
              binding="basicHttp"
              bindingConfiguration="basicHttpBinding"
              contract="IHelloWorldService" />
  </service>
</services>
```

This is a simple WCF service. To use it, you can use a client proxy.

```csharp
ChannelFactory<IHelloWorldService> factory = new ChannelFactory<IHelloWorldService>("service.svc");
IHelloWorldService channel = factory.CreateChannel();
Console.WriteLine(channel.HelloWorld("World"));
```

This is how you use a WCF service.

In the next example, we'll build a more complex WCF service. This service will have multiple methods, and it will use data types.

```csharp
[ServiceContract]
public interface ICalculatorService
{
    int Add(int a, int b);
    int Subtract(int a, int b);
    int Multiply(int a, int b);
    int Divide(int a, int b);
}

public class CalculatorService : ICalculatorService
{
    public int Add(int a, int b) { return a + b; }
    public int Subtract(int a, int b) { return a - b; }
    public int Multiply(int a, int b) { return a * b; }
    public int Divide(int a, int b)
    {
        if (b == 0) throw new ArgumentException("Cannot divide by zero.");
        return a / b;
    }
}
```

This is a more complex WCF service.

In the next example, we'll build a WCF service that uses custom objects.

```csharp
[DataContract]
public Person
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Email { get; set; }
}

[ServiceContract]
public interface IPersonService
{
    Person GetPerson(int id);
}

public class PersonService : IPersonService
{
    public Person GetPerson(int id)
    {
        return new Person { Id = id, FirstName = "John", LastName = "Doe", Email = "john.doe@example.com" };
    }
}
```

This is a WCF service that uses custom objects.

# Building Web Services with REST

REST is the most popular way to build web services. It's simple and easy to use. In this chapter, we'll learn how to build a simple REST service.

To build a REST service in ASP.NET, you can use Web API.

```csharp
[RoutePrefix("api/[controller]")]
public class HelloController : ApiController
{
    [HttpGet("hello/{name}")]
    public string HelloWorld(string name)
    {
        return "Hello " + name;
    }
}
```

This is a simple REST service. To use it, you can use an HTTP client.

```csharp
HttpClient client = new HttpClient();
string result = await client.GetStringAsync("http://localhost:port/api/hello/World");
Console.WriteLine(result);
```

This is how you use a REST service.

In the next example, we'll build a more complex REST service. This service will have multiple endpoints, and it will use custom data types.

```csharp
[RoutePrefix("api/[controller]")]
public class PeopleController : ApiController
{
    [HttpGet("people/{id}")]
    public IHttpResult GetPerson(int id)
    {
        return Ok(new Person { Id = id, FirstName = "John", LastName = "Doe", Email = "john.doe@example.com" });
    }

    [HttpPost("people")]
    public IHttpResult CreatePerson(Person person)
    {
        // Save the person to the database.
        return Created(person);
    }
}
```

This is a more complex REST service.
