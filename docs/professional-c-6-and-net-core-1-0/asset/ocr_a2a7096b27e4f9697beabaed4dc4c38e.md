method. According to the asynchronous pattern, the BeginGreeting method receives a string parameter in addition to AsyncCallback and object parameters and returns IAsyncResult. The EndGreeting method returns the result from the Greeting method—a string—and receives an IAsyncResult parameter. This way the synchronous method Greeting was made asynchronous just by using a delegate.

```
private Func<string, string> greetingInvoker = Greeting;
```

```
private IAsyncResult BeginGreeting(string name, AsyncCallback callback, object state)
{
	return greetingInvoker.BeginInvoke(name, callback, state);
}
```

```
private string EndGreeting(IAsyncResult ar)
{
	return greetingInvoker.EndInvoke(ar);
}
```

Now the BeginGreeting and EndGreeting methods are available, and these should be converted to use the async and await keywords to get the results. The TaskFactory class defines the FromAsync method that allows converting methods using the asynchronous pattern to the TAP.

With the sample code, the first generic parameter of the Task type, Task<string>, defines the return value from the method that is invoked. The generic parameter of the FromAsync method defines the input type of the method. In this case the input type is again of type string. With the parameters of the FromAsync method, the first two parameters are delegate types to pass the addresses of the BeginGreeting and EndGreeting methods. After these two parameters, the input parameters and the object state parameter follow. The object state is not used, so null is assigned to it. Because the FromAsync method returns a Task type, in the sample code Task<string>, you can use an await as shown:

```
private static async void ConvertingAsyncPattern()
{
	string s = await Task<string>.Factory.FromAsync<string>(
		BeginGreeting, EndGreeting,"Angela", null );
	WriteLine(s);
}
```

# Error Handling

Chapter 14, “Errors and Exceptions,” provides detailed coverage of errors and exception handling. However, in the context of asynchronous methods, you should be aware of some special handling of errors.

The sample code for all the ErrorHandling sample makes use of these dependencies and namespaces:

# Dependencies

NETStandard.Library