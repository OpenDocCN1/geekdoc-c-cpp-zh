# 364 | CHAPTER 10 ASP.NET AJAX

variable names, methods, services, and so on that it finds in your code. Since VS 2010, Microsoft has improved IntelliSense even further by improving the performance and the accuracy of the items shown in IntelliSense.

To see how the actual page works, and how it accesses the web service, take a look at the code in the `script` block.

The first code you need to look at is the helloWorld:

```
function helloWorld() {
    var yourName = document.getElementById('yourName').value;
    NameService.HelloWorld(yourName, helloCallback);
}
```

First, this code gives a reference to the text box you created earlier. Then you can access its value property to get the name under.

This name is sent to the web service method HelloWorld with the following code:

```
NameService.HelloWorld(yourName, helloCallback);
```

The first argument of the call to HelloWorld is the argument that the web service expects: a string value. The second argument, helloCallback, is a reference to another JavaScript method that is triggered when the service returns the result. By design, the call to the service is made asynchronously. This means that the service is made in a separate thread and the helloMethod exits shortly afterward. Because it can potentially take a long time for the web service to respond, you must designate a method that is responsible for handling the response when it comes back from the service. In this case, the responsible method is called helloCallback.

In addition to this success callback, you could add another one that is triggered when the web service fails some way; for example, because the connection is down or the service throws an exception. In this case, the call to HelloWorld would look like this:

```
NameService.HelloWorld(yourName, helloCallback, helloErrorCallback);
```

The HelloWorldCallback function could then look like this:

```
function helloErrorCallback(error) {
    alert(error.message);
}
```

The error that is passed to this method has convenient methods and properties to display information about the exception. In the example, you use get_message() to get the original exception that occurred on the server. You should use this only during development to figure out the actual error. In Chapter 18 you learn more about dealing with errors at the server so the details are never sent to the client's browser.

If everything goes according to plan, the call to HelloWorld triggers the web service method HelloWorld. This method receives the name and returns a friendly welcome message.

The String.Format method takes a string that contains numeric placeholders wrapped in a pair of curly braces ({}). Then for each numeric value, you supply a value as subsequent parameters. In the