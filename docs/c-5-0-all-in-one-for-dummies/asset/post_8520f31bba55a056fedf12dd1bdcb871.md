
3. Right-click the `SharpAsmx` project and add an Entity Data Model by selecting Add New Item and picking ADO.NET Entity Data Model from the list.

(It’s under Data.) I named it SHARP.edmx.

4. When the Entity Data Model wizard appears, select Generate from Database and click Next.

5. In Choose Your Data Connection, pick the `ConferenceDb` you added in Step 1; keep the rest of the defaults.

6. When it asks you to copy the file to your project, choose No.

You don’t need copies of the database floating around.

7. In Choose Your Database Objects, pick all the tables except sysdiagrams and change the Model Namespace to ConferenceDB.

An example appears in Figure 2-3.

8. Click Finish.

That’s how you set up an ASMX web service project. You have a data source, an entity model (you could use your organization’s domain model, or hand-rolled procedures and ADO.NET, or whatever), and a starting point for the service.

Next, you set up some services that make sense of your user interface. There are two schools of thought on this. First, you can roll up the entity model in the service signature itself. Second, you could write a separate business layer and just call the Business Layer (BL) methods with the services.

![](img/80ff26f06fc9ab951e1cd4257b867366_784_0.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_784_1.png)

Figure 2-3:
Adding the Sharp tables to the model.

The deciding factor is reuse. If you will later need to roll exactly this logic into a standalone application (anything that won’t use the services), then make a separate BL. For simplicity, we will do the former.

1. Using the default template, delete the default <code>HelloWorld</code> method and put in a method signature for a new <code>conferencesAtLocation</code> method.
It will accept a <code>conferenceId</code> (maybe from website navigation) and return a list of conferences at that location.
<pre><code>public List&lt;Conference&gt; conferencesAtLocation(int locationId)
{
}</code></pre>

2. The first step is just to get the entities from the Entity Data Model.
Do so by adding the bold lines. They set up a context for the Entity Framework. Then get the list of conferences:
<pre><code>public List&lt;Conference&gt; conferencesAtLocation(int locationId)
{
    ConferenceDbEntities conferenceContext = new ConferenceDbEntities();
    DbSet&lt;Conference&gt; allConferences = conferenceContext.Conferences;
}</code></pre>

3. Write a Linq query to just get the conferences with the <code>locationId</code>.
This is in the bold lines:
<pre><code>public List&lt;Conference&gt; conferencesAtLocation(int locationId)
{
    ConferenceDbEntities conferenceContext = new ConferenceDbEntities();
    DbSet&lt;Conference&gt; allConferences = conferenceContext.Conferences;
    <b>var conferenceQuery = from c in allConferences
                              where c.LocationId == locationId
                              select c;</b>
}</code></pre>

4. In order to use the results of the Linq query, you must use an iterator
and dispose of the context; finally, you return the results.
These steps are in the bold lines added:
<pre><code>public List&lt;Conference&gt; conferencesAtLocation(int locationId)
{
    ConferenceDbEntities conferenceContext = new ConferenceDbEntities();
    DbSet&lt;Conference&gt; allConferences = conferenceContext.Conferences;
    var conferenceQuery = from c in allConferences
                         where c.LocationId == locationId
                         select c;
    <b>List&lt;Conference&gt; locationConferences = conferenceQuery.ToList();
    conferenceContext.Dispose();</b>

    <b>return locationConferences;</b>
}</code></pre>

5. To make it a web service, you need to add the `WebMethod` decorator on the method signature, and you are done:

```csharp
[WebMethod]
public List<Conference> conferencesAtLocation(int locationId)
{
    ConferenceDbEntities conferenceContext = new ConferenceDbEntities();
    DbSet<Conference> allConferences = conferenceContext.Conferences;
    var conferenceQuery = from c in allConferences
                          where c.LocationId == locationId
                          select c;
    List<Conference> locationConferences = conferenceQuery.ToList();
    conferenceContext.Dispose();

    return locationConferences;
}
```

6. Press F5 to run the test page and click the `conferencesAtLocation` method link; enter 3 into the Test field.

The result should come back like Figure 2-4, if everything is good.

So what about all that other stuff that goes into SOAP? Security, transactions, and like that? It’s all baked in, but it’s well beyond the scope of this book.

For instance, check out the `SoapHeader` attribute. It allows you to specify even the most complex security attributes on your web methods. There’s more, too. Check out MSDN.

![](img/80ff26f06fc9ab951e1cd4257b867366_786_0.png)

Figure 2-4: Results of the service.

3. **Click the Discover button.**

Visual Studio finds all the services in your solution. In a real project, you probably would put a URL in the Address text box.

4. **Select the `Registration.asmx` service and set the Namespace to `SharpReference`.**

An example is shown in Figure 2-6.

![](img/80ff26f06fc9ab951e1cd4257b867366_788_0.png)

**Figure 2-6:** Adding a service reference.

5. **Click OK.**

Visual Studio does a ton of work for you here. There is no magic — Visual Studio reads the WSDL of the service referenced and builds a proxy just as though it were a service written in C++ or Java.

As such, the objects returned to you will be more along the lines of a service than what you would expect in C#, especially as delivered by ASMX. The code in the console application to consume your now-proxied service looks like this:

```csharp
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
```

```csharp
SharpReference.conferencesSoapClientServiceReference =
    new SharpReference.conferencesSoapClient();
SharpReference.Conference[] conferences =
    serviceReference.conferencesAtLocation(3);
Console.WriteLine("There will be {0} conferences at location number
3.", conferences.Length);
Console.ReadKey();
    }
}
}
```

Notice that the conferencesAtLocation method now returns an array rather than a List<Conference>. The consuming language doesn't have to have generics, but it does have to have arrays (if it conforms to WS-I). That's the only assumption we can make. (See Figure 2-7.)

![](img/80ff26f06fc9ab951e1cd4257b867366_789_0.png)

Right-click the console application and press F5. The console application should start, and it should find the two rows in the array just as it would in the list.

## Chapter 3: Building Web Services with WCF

### In This Chapter

- Becoming acquainted with WCF
- Building a WCF service
- Configuring a new service
- Deploying a new service

Windows Communication Foundation is just that — the foundation for communication between Windows computers. It just so happens that thanks to open standards like SOAP and REST, WCF can communicate with other software systems (even non-Windows systems).

Although ASMX was really designed to make public services — such as, for instance, adding an API to a simple web application — WCF is a complete distributed computing platform for Windows.

In the early days of .NET, there was a technology called .NET Remoting that replaced DCOM. DCOM was Distributed COM, or the common accepted way to communicate between distributed components. It was replaced by Remoting when .NET came out. Remoting basically took the principles of DCOM and migrated them to .NET.

WCF isn't like that. WCF is a complete rethinking of distributed computing, based on the understanding that computing is becoming more and more distributed. New protocols for communication come out every day.

The goal here then is to define the differences between ASMX and WCF, and see that WCF is a true communications protocol and that ASMX is solely for adding services to websites. You can use either technology for both tasks, but one is certainly more suited than the other for each.

In this chapter, I look at why WCF works well and then build the SHARP service for a variety of service types. You don't have to change a lick of code to do it, either. It's all in the configuration.
