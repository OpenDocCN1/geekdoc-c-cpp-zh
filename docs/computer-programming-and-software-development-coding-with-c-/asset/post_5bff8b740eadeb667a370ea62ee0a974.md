
out. The references to the project for the CSV reader, the Service reader, and the SQL reader are not being used. That means we can get rid of them. And as a shortcut, I'll use Ctrl+dot, and you'll see there's an option to remove unnecessary usings. And what that leaves us with is that our PeopleController is only referencing the interface and the factory. It doesn't care about any of the specific data readers.

![](img/0155736aec718cf18821e9f10a5d308d_936_0.png)

And we can go a step further in our project. I can go to the project references and remove links to the CSV, Service, and SQL projects. This means that our PeopleViewer project does not have any direct knowledge of any specific data readers. And if we run the application again, we'll see that it still works. We can still get data from our web service, from our text file or from our SQL database. We only care about the interface in this project. We have the piece of functionality that we need, the ability to call the GetPeople method. We do not care what object we have as long as it has a GetPeople method. This gives us a better separation of concerns and puts responsibilities where they belong. It does not make a whole lot of sense for one application to reference three different data sources like we have here. Most likely our application will need access to one data source based on our client's needs, and we'll look at that in a future demonstration. By using our data reader interface, we are able to remove references to any specific data readers in our calling code.

```
private IActionResult PopulatePeopleView(string readerType)
{
    IPersonReader reader = readerFactory.GetReader(readerType);
    IEnumerable<Person> people = reader.GetPeople();
    ViewData["ReaderType"] = reader.GetType().ToString();
    return View("Index", people);
}
```

The PopulatePeopleView method references IPersonReader, and it asks the factory method to provide an object that implements that. When we call the GetPeople method, we know that we will get an IEnumerable back since that is what is specified by the interface. We do not care about the details of how that happens. We just care that it does happen. The details can be someone else's responsibility. This also means that if we need to switch to a different SQL technology, for example, one that uses Oracle or a MySQL database, we just need to update the factory method to create the right data reader. Our calling code does not need to care about that. I have had to make a change like this from a Microsoft SQL Server database to an Oracle database, and I will talk about that a bit more in the next chapter. In this chapter, we have focused on the how of interfaces. Specifically, we saw how to create a repository interface. We simplified the CRUD operations down to just the read operations that we needed, and the interface represents how we interact with the data. We saw how to implement the interface. We created a service reader and saw how Visual Studio gives us an easy way to stub out all the members of an interface. In addition to the service reader, we use data readers to access a text file and a SQL database. With the

interface in place, it was easy to eliminate code duplication. The interface became a parameter that we could use to create a consolidated method. Then we took that one step further to create a factory method. This moved the details out of our main application so that we could focus on the important functionality, getting a collection of person objects that we can display for our users. As mentioned, we probably only want to access a single data source from our application, but we may need to change that data source. In the next chapter, we will look at how interfaces can help us choose the functionality our application will use at runtime.

## Chapter 5 Dynamic Loading and Unit Testing

We have created several different data readers to implement our interface. Whenever we use them, we have compile time references to the concrete classes, but we can take this a step further. We can update our application so that it does not know anything about the specific data reader classes at compile time. Instead, we dynamically load a data reader when the application runs. This removes the connection between our application and any specific data reader implementation, and this also makes our code easier to unit test. This time, we will look at more of the how and the why of interfaces. We will do this by looking at some scenarios. The first is to change a data reader of an internal application without needing to recompile or redeploy. The second scenario puts our application into the hands of multiple clients, and each one has their own way to store data. By using the interface only, we can focus on the important functionality and not worry about the details. We will do this by updating our code to make decisions when our application runs rather than when it is compiled. This means that we can change the behavior of the application without recompiling. Since we do not have to recompile to make these changes, our application is easier to maintain and deploy, and it also makes unit testing easier. Unit testing has been a huge benefit in my development work. We will see how interfaces can make our unit tests easy to read, write, and understand. So let's keep going to see how we can get all of these benefits. The first scenario is one I came across while working

as a corporate developer. One of my applications connected to a database to get some data. Initially, the database ran on Microsoft SQL Server, but then the system was going through an update, which included moving the database to an Oracle server, and the new database also had a different layout of tables and fields. One way I could have made the transition is to replace the Microsoft SQL Server code with Oracle code. The thing I did not like about this approach is that I would need to schedule the deployment of my application to match the application deployment, so instead, I took a different approach. I added some configuration to the application to specify whether the application should use the Microsoft SQL database or the Oracle database. During testing, I could change the configuration back and forth, either to connect to the test Microsoft SQL database or to the test Oracle database. This let me make sure that the functionality of my application was the same in either environment. Once my updated code was ready, I went through our deployment process to get the application onto our production servers, and I had the configuration pointed at the Microsoft SQL Server database. Then during the deployment of the system, all I had to do was change the configuration to point to the new Oracle database. This greatly simplified the deployment for this application, and fortunately, things went smoothly. For the next sample, we will do something similar with our example application. We will add code that lets us pick which data reader to use based on configuration. By setting the configuration, we can use the service data reader, the CSV data reader, or the SQL data reader, and we can do this by changing configuration. We do not need to recompile or redeploy the application, and as we'll see, the data reader interface plays a key role in making this possible. In the following demonstrations, I used Visual Studio 2019. Running the projects is a little bit different in Visual Studio Code. Now let's go to the code. In

this sample, we will update our application to look in Configuration to decide which data reader to use, in the code, we will update the controller to use the new Configuration, and we will update the user interface, the view, to add a new link to our screen. This will give us the ability to switch to a different data reader without recompiling our application. We only need to update the Configuration to use a new data reader. Here we are back in Visual Studio with the extensibility solution open. This code is in the same state that we left it in the previous demonstration, three links that use three different data readers to get data.

```
```csharp
using PersonReader.CSV;
using PersonReader.Interface;
using PersonReader.Service;
using PersonReader.SQL;
using System;

namespace PersonReader.Factory
{
    public class ReaderFactory
    {
        public IPersonReader GetReader(string readerType)
        {
            switch (readerType)
            {
                case "Service": return new ServiceReader();
                case "CSV": return new CSVReader();
                case "SQL": return new SQLReader();
                default:
                    throw new ArgumentException($"Invalid reader type: {readerType}");
            }
        }
    }
}
```
```

We will change this so the data reader is selected based on what is in a Configuration file. This will let us change the behavior of our application without recompiling it, so let's start by adding Configuration. We do need to know what the valid values are, and for that, we can look in our factory method. So let's go to the PersonReader.Factory project and open the ReaderFactory. This shows us our three current valid values, Service, CSV, and SQL. So let's go
