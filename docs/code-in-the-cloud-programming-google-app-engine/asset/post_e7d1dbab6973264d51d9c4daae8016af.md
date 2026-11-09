
In addition, if you look on the left side of the panel, there’s a list of different categories that you can use to drill down and get more precise information. You can check how you’re doing on your quotas; you can get very precise information about your instances; you can check your task queues; and so on.

### 18.2 Peeking at the Datastore

As we’ve seen throughout this book, most of App Engine isn’t really anything new. Wherever possible, App Engine tries to reuse standard technologies to allow you to write cloud applications. The one place where App Engine is really different, the one really novel thing in App Engine, is the datastore. Most cloud application frameworks provide you with access to some kind of lightweight relational database like MySQL. But App Engine goes a very different route, storing things in Google’s Bigtable using the datastore.

So one really important thing as you administer your App Engine application is to understand how your data is stored and how that storage model affects your resource usage.

In the App Engine control panel, there are a set of views for letting you peek and probe at how your application is using the datastore.

The easiest thing to see is how your data is indexed. If you just click on Datastore Indexes, it will show you a list of the data types that you’re storing and which fields of them are indexed. This is most valuable early in the development process. Datastore automatically indexes some fields based on your queries. By looking at this view, you can see what indices you have and what indices you don’t have.

You can also browse your way through all of the objects that you’ve stored. If you click on Datastore Viewer, you can see a list of all of the objects in your datastore, categorized by type. You can also find specific objects: if you click on the Options link in the datastore viewer, it shows you a GQL query that was used to generate the current view, and you can edit the query. For example, in my chat application’s datastore, there are PChatMessage objects, and PChatRoom objects. I can look at all of the chat messages that were sent by me by entering a query like `SELECT * FROM PChatMessage where senderName='markcc'`.

Finally, you can see how much storage objects are taking—including the metadata for their indices—by checking under Datastore Statistics.

### 18.3 Logs and Debugging

When you’re having trouble with your application, the most useful thing on the entire control panel is logs. Logs give you a way of looking into your running application in almost the way that you could with a local debugger. Every time anything goes wrong in your application, App Engine will generate a log entry for it; by viewing the logs, you can see what happened.

For example, when I open the Logs view, I can see that I made a mistake in that chat application. The template that I used for generating chat views says that there should be a favicon; but there is no favicon available. So every pageview request ends up generating an error due to the missing favicon. That doesn’t stop my application from working. In fact, I didn’t even know that I’d made that mistake before the first time I checked my logs! But that’s exactly why logs are so valuable: in App Engine, you can’t directly watch your application run the way you could if it were on your own computer. It’s running somewhere else on a machine you can’t access directly. But the logs provide you with a valuable tool that allows you to get as much information about your running application as you want.

Of course, App Engine isn’t going to automatically tell you everything. It can’t know exactly what bits of information you’re going to want. So all that it does automatically is record errors that it’s aware of. If your application tries to access data from the datastore that it can’t find, App Engine knows about it, and it can generate an entry in your log. But if your application successfully retrieves information from the datastore, but due to an error in the query, it’s not the correct information, App Engine doesn’t know, and so it doesn’t automatically log anything.

You can insert logging commands into your application using your language’s standard logging support (like java.util.logging in Java); all of the log entries are viewable by clicking on the Logs entry in the control panel. This is your most valuable tool for debugging: you can see exactly what your application is doing by generating log entries.

For example, the version of my chat application that’s deployed right now contains an error. If I give it a long chat message, it will fail to process it correctly. Why?

When I look in the default logs, I see a bunch of entries like Figure 18.3, on the following page, all complaining about not being able to process chat messages that are longer than 500 characters, because the datastore model specifies the message content as a string property, and strings can’t be longer than 500 bytes. But my chat messages aren’t 500 characters long!

![](img/5089b2737348ba4c97c74871e2878f24_280_0.png)

Figure 18.3: A log entry from the control panel log viewer

For this problem, the default log message is enough to clue me in, but suppose it wasn’t. Maybe I thought that the chat messages weren’t that long. I could add logging code to my application. First, I’d need to declare the logger in my source file. So I’d add the following to com.program.google.appengine.api... at the very end, right before the closing brace:

```java
private static java.util.logging.Logger logger =
    java.util.logging.Logger.getLogger(ChatSubmissionServiceImpl.class.getName());
```

And then, inside of the postMessage method, I could add a logging statement:

```java
logger.info("Chat message size = " + message.getMessage().length() +
            " with body \"" + message.getMessage() + "\"");
```

With that statement added, every single post message will generate a log entry containing the length and content of a posted message. With that, I could confirm that the messages really were more than 500 characters.

You should, however, be a bit careful about adding logging to your application. It’s an incredible tool. But logging takes CPU time, which does count against your quota. You don’t need to worry about space; App Engine will only keep a certain number of your most recent log entries, automatically discarding older ones. So doing too much logging can, quite literally, cost you money. Not much, but it is a real consideration.

More importantly, the logs are your primary tool for understanding what’s going on in your application. If you generate a ton of log entries for every trivial thing, then you’re crowding your logs with irrelevant data. That data can make it hard to find the important entries—or if there are really a lot of them, they can even crowd out the relevant ones entirely! The rule of thumb is don’t log anything that you don’t actively want to read—don’t write log entries that you know you’re never going to look at. But when you’re having a problem, add log statements so that you can see what’s going on and then hit the logs in your control panel while you’re debugging.

### 18.4 Managing Your Application

The control panel contains a collection of settings that help you manage your application. There are four views that you can use for managing things: Application Settings; Permissions; Versions; and Admin Logs.

The Application Settings view gives you access to a set of basic settings for your application. It includes the following:

- *Application Title.* This produces the name of your application in an editable text box. To change the application name, you can just change the contents of the text box, and click Save Settings.

- *Configured Services.* If your application uses any services, like email or XMPP (chat), the services will be listed here, with any options that you can configure.

- *Cookie Expiration.* App Engine uses cookies for authentication of users. You can choose between setting the cookies so that users stay logged in for one day or for one week.

- *Disable or Delete Application.* If you want to either temporarily or permanently shut down your application, this is the place to do it. If you click Disable Application, you’ll first be taken to a confirmation dialog to ensure that you really want to shut the application down. If you confirm it, the application will be disabled, and the Application Settings view will be changed so that it contains two items—one to relaunch the application and one to permanently delete it.

- *Domain Setup.* If you want to run your application on your own domain, you can tell App Engine about the domain here. Currently, you can buy
