+   - Loosely coupled: They don't require a constant connection to the server
+   - Contract driven: They provide an interface that describes all of their functionality
+   - More likely to be chunky, not chatty: Rather than lots of properties with single values, they provide big methods that return collections.

I discuss these topics more fully in the sections that follow.

# Loosely coupled

Because Web services are, like Web applications, loosely coupled, Web service conversations aren't guaranteed to make sense. You might get a sentence from three minutes ago, after four other sentences have gone past, or you might not hear from them again after the first line.

When you stop to think about it, loose coupling makes sense: Web service calls are just like navigation in a Web page. Sometimes you click a link and then close your browser, and sometimes you click the link twice. Web applications are up to the whim of the user, and so are Web services.

For this reason, a client of a Web service must be loosely coupled to the service. For example, you don't want to make a user wait until a Web service call is complete. You must call it asynchronously and have the result show up when it is ready.

Fortunately, .NET handles the asynchronous call. You just tell your application that you're calling a service asynchronously and then provide a delegate for the service to call when it's ready. As long as you handle the code properly, the service will work as expected.

In this example, you can see that we implemented the loose coupling with an asynchronous call:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            //Here YOU are calling the service
            asynchronously.
```