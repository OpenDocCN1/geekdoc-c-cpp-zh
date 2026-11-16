
```
}
[HttpPost]
public ActionResult<Product> CreateProduct([FromBody] Product product)
{
    // ... create a new product in the database
}

[HttpPut("{id}")]
public IActionResult UpdateProduct(int id, [FromBody] Product product)
{
    // ... update an existing product in the database
}

[HttpDelete("{id}")]
public IActionResult DeleteProduct(int id)
{
    // ... delete a product from the database
}
}
```

In this example, we define action methods for retrieving all products (GetAllProducts), retrieving a product by ID (GetProductById), creating a new product (CreateProduct), updating an existing product (UpdateProduct), and deleting a product (DeleteProduct). The attribute routing attributes ([HttpGet], [HttpPost], [HttpPut], [HttpDelete]) specify the HTTP methods and routes for each action.

## Best Practices for API Controllers

- Use nouns for resource names: Represent resources using nouns in your routes (e.g., /products, /orders) to promote clarity and consistency.
- **Leverage HTTP verbs:** Use the appropriate HTTP verbs (GET, POST, PUT, PATCH, DELETE) to indicate the intended action on a resource.
- **Return appropriate status codes:** Utilize HTTP status codes to communicate the outcome of a request to the client.
- **Validate input:** Always validate user input to ensure data integrity and prevent potential security vulnerabilities.
- **Handle errors gracefully:** Implement error handling mechanisms to catch and handle exceptions, returning informative error messages to the client.
- **Version your API:** If your API is likely to evolve over time, consider versioning it to avoid breaking changes for existing clients.

In this section, we've explored the process of creating API controllers in ASP.NET Core 3, leveraging the `ApiController` attribute and attribute routing to build RESTful web services. We've learned how to define action methods, handle requests, generate responses, and ensure data validation and security. Armed with this knowledge, you're now equipped to craft well-designed and maintainable APIs that seamlessly integrate with other systems and services, empowering your applications to communicate and exchange data effectively.

## Handling HTTP Requests and Responses

In the realm of web APIs, the exchange of information between clients and servers revolves around HTTP requests and responses. These messages, adhering to the HTTP protocol, carry data, metadata, and instructions that facilitate communication and enable the seamless flow of information across the web. In this section, we'll delve into the intricacies of handling HTTP requests and responses in ASP.NET Core 3, exploring how to parse incoming data, generate appropriate responses, manage content negotiation, and ensure efficient and secure communication between your API and its clients.

## Understanding HTTP Requests

An HTTP request is a message sent from a client, such as a web browser or another application, to a server, requesting a specific action or resource. It typically consists of the following components:

- **Method:** The HTTP method (e.g., GET, POST, PUT, PATCH, DELETE) indicating the intended action on the resource.
- **URI (Uniform Resource Identifier):** The address of the resource being requested, including the hostname, path, and any query parameters.
- **Headers:** Metadata providing additional information about the request, such as the content type, authorization credentials, or client preferences.
- **Body (Optional):** Data sent with the request, typically used for POST, PUT, and PATCH requests to create or modify resources.

## Parsing Incoming Data

ASP.NET Core 3 provides powerful model binding capabilities to automatically extract data from incoming requests and populate corresponding objects in your controller action methods. It supports binding data from various sources, including:

- **Request Body:** For POST, PUT, and PATCH requests, data is typically sent in the request body, often in JSON or XML format. You can use the [FromBody] attribute to bind this data to a parameter in your action method.
- **Query String:** Query parameters are appended to the URI after a question mark ( ? ) and are typically used for filtering, sorting, or pagination. You can access query parameters using the Request.Query property in your controller.
- **Route Values:** Route values are extracted from the URI based on the defined routes. You can access route values using parameters in your action method signature.
- **Headers:** You can access request headers using the Request.Headers property in your controller.

## Generating HTTP Responses

Once your controller action method has processed the request and interacted with the model, it needs to generate an appropriate HTTP response to send back to the client. ASP.NET Core 3 offers various ways to create responses:

- **Action Results:** Action methods typically return action results, which represent the response to be sent to the client. Common action result types include Ok, NotFound, BadRequest, Created, and NoContent.
- **Object Results:** You can also return objects directly from your action methods. The framework will automatically serialize the object into the appropriate format (e.g., JSON) based on content negotiation.
- **Custom Responses:** For more fine-grained control, you can create custom responses using the Response object in your controller.

## Content Negotiation

Content negotiation is the process of determining the best representation of a resource to send to the client based on its preferences. Clients can specify their preferred media types (e.g., application/json, application/xml) in the Accept header of the request. ASP.NET Core 3 supports content negotiation out of the box, automatically selecting the appropriate formatter based on the client's preferences.

## Error Handling and Status Codes

When errors or unexpected situations occur, it's important to return appropriate HTTP status codes to communicate the outcome of the request to the client. Use 4xx status codes for client errors (e.g., 400 Bad Request, 404 Not Found) and 5xx status codes for server errors (e.g., 500 Internal Server Error). You can also include additional information in the response body, such as error messages or details, to aid in troubleshooting.

In this section, we've explored the essential aspects of handling HTTP requests and responses in ASP.NET Core 3. We've learned how to parse incoming data, generate appropriate responses, manage content negotiation, and ensure efficient and secure communication between your API and its clients. Armed with this knowledge, you're now equipped to build robust and well-designed APIs that seamlessly handle a variety of requests and provide meaningful responses, fostering effective communication and data exchange in the interconnected world of web services.

## Consuming APIs from Web Applications

In the interconnected landscape of modern web development, APIs (Application Programming Interfaces) serve as the conduits for communication and data exchange between disparate systems and services. Consuming APIs from web applications empowers you to tap into a wealth of external data and functionality, enriching your own projects with features and information that would otherwise be difficult or time-consuming to develop from scratch. In this section, we'll explore the techniques and best practices for seamlessly integrating API consumption into your ASP.NET Core 3 web applications, enabling you to harness the power of external APIs and create dynamic and data-driven user experiences.

## The HttpClient: Your API Communication Tool

The HttpClient class in .NET provides a versatile and efficient way to send HTTP requests and receive HTTP responses from web APIs. It handles the low-level details of network communication, allowing you to focus on interacting with the API's endpoints and processing the returned data.

Let's see a simple example of using HttpClient to consume an API:

```
C#
using System.Net.Http;
using System.Threading.Tasks;
using Newtonsoft.Json; // For JSON deserialization
// ...
public async Task<IActionResult> GetProductsFromApi()
{
    using (var httpClient = new HttpClient())
```
