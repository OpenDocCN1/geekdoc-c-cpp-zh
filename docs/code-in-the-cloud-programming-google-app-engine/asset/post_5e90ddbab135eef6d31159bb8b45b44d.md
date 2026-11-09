
## 9.4 Testing and Deploying with GWT

Now that we've got a basic GWT application, let's run it. Just like in Python, there are two ways of running a GWT application in App Engine: a local mode, where the application runs on your machine, and a deployed mode, where the application runs in the App Engine cloud.

The local mode in GWT is very different from the local mode in Python. In Python, local mode was nice for testing without deploying, but it didn't really afford the same level of support for debugging. But with GWT, in the local mode, both the client and the server run in Java, and we can use all of the capabilities of Eclipse to debug the GWT application. That makes a huge difference: we have full access to breakpoints, traces, stepping, and all of the other Java debugging tools.

To run in local mode using Eclipse, go to the Run menu and pick Run As.../Web Application. GWT will open a local simulated browser environment to display the client and start a local Tomcat web server to execute the server.

To deploy it to App Engine, go to the Package Explorer view and right-click the project. In the project menu that comes up, there's a Google submenu. Just select Deploy to App Engine, and your program will be live in the App Engine cloud. If there's any information about the project that it needs, it will prompt you to fill it in the first time you run the deploy command.

We finished our first basic GWT application. It isn't as full-featured as our Python chat application yet, but it's got a better UI and a cleaner communication layer. In the next chapter, we'll take what we've learned about GWT and use it to build a Java version of our chat application. In the process, we'll learn about the Java interface to the datastore and about the restrictions that GWT puts on server-side Java code.

## Chapter 10: Managing Server-Side Data

In the previous chapters, we examined the pieces of a basic GWT application in App Engine. We built a GUI, set up a simple RPC, and strung all of the plumbing together to get an application working. In this chapter, we’re going to implement our chat program using GWT. We won’t spend much time looking at how to build the GUI—there are entire books on building GUIs in GWT, and GWT’s own documentation of its UI classes is excellent. What we’ll spend most of our time on is *datastore*, the mechanism that lets us work with persistent data in App Engine. Just like in Python, we need to do some extra work to make classes persistent and queryable. Now we’ll look at how to do that using Java.

We’ll also touch on some other issues of the server-side plumbing in the Java side of App Engine. Specifically, App Engine puts some restrictions on what code can do and how it can run in the App Engine cloud environment, and we’ll examine what those restrictions are and what effect they have on how we write the server side of our App Engine applications.

### 10.1 Data Persistence in Java

If you look back at Chapter 4, *Managing Data in the Cloud*, on page 53, you’ll remember that we needed to do some extra work in our Python code to store data and to make things work correctly in the cloud. The same thing is true in Java. Unfortunately, this is one of the places where the static typing of Java makes things a bit more cumbersome. The basic back-end datastore used by App Engine is exactly the same as in Python, but making it work with Java takes a bit more thought. It's not difficult, but there's a bit more boilerplate that we need to put into our code. As usual, Eclipse can take care of a lot of that for us. Let's get started without Eclipse's help, though. We'll write everything by hand, so that we understand all of the details.

In typical Google style, what App Engine does to make datastore work with Java is grab a standard Java API—Java Data Objects (JDO)—and pick out a useful subset of its functionality. JDO is a hugely complex, bloated API (typical of standards). But there's a kernel of goodness to it. App Engine uses that kernel.

Below, we'll see how JDO persistence works for describing persistent objects and for storing, querying, and retrieving them.

### Storing Java Classes

In Python's datastore interface, we created a persistent class by adding attributes to the class object. In Java, we'll do something similar—but in Java, attributes are added through the use of annotations in the class declaration. It's easiest to describe by example, so we'll take our chat message and translate it into a data object:

Download `workspace/PortalChat/src/com/progprog/aebook/persistchat/ChatMessage.java`

```java
package com.progprog.aebook.persistchat;

import java.util.Date;

import javax.jdo.annotations.IdGeneratorStrategy;
import javax.jdo.annotations.IdentityType;
import javax.jdo.annotations.PersistenceCapable;
import javax.jdo.annotations.Persistent;
import javax.jdo.annotations.PrimaryKey;

import com.google.appengine.api.datastore.Key;

@PersistenceCapable(identityType = IdentityType.APPLICATION)
public class ChatMessage {

    public ChatMessage() {
    }

    public ChatMessage(String sender, String msg, String chatname) {
        this.senderName = sender;
        this.message = msg;
        this.chat = chatname;
    }

    @PrimaryKey
    @Persistent(valueStrategy = IdGeneratorStrategy.IDENTITY)
    private Key key;

    @Persistent
    protected String senderName;

    @Persistent
    protected String message;

    @Persistent
    protected String chat;

    @Persistent
    protected long date;

    public Key getKey() {
        return key;
    }

    public String getSenderName() {
        return senderName;
    }

    public void setSenderName(String senderName) {
        this.senderName = senderName;
    }

    public String getMessage() {
        return message;
    }

    public void setMessage(String message) {
        this.message = message;
    }

    public String getChat() {
        return chat;
    }

    public void setChat(String chat) {
        this.chat = chat;
    }

    public long getDate() {
        return date;
    }

    public void setDate(long date) {
        this.date = date;
    }
}
```

Let’s take a closer look at this example:

- 1. For a Java object to be stored in the App Engine datastore, its class must be declared as persistent. In JDO, you do this by attaching a `@PersistenceCapable` annotation. In full JDO, we need to declare an identity type. App Engine only supports `IdentityType.APPLICATION`, but because Java’s type system requires annotations to match their declaration, the field must always be declared.

  To be able to store, retrieve, or search for a particular object, the object must have a unique key that is used to identify it. In Python, when we defined a persistent object, the framework automatically added an invisible key field that was used by datastore. In Java, everything needs to be declared statically. So we need to manually insert the key declaration in the source code and annotate it as being a key. We mark it as a key using the `@PrimaryKey` annotation, and we tell it that the way to compare primary keys is through object identity using the `valueStrategy = IdGeneratorStrategy.IDENTITY` attribute of the `@Persistent` annotation.

- 2. Each field of a persistent object that should be stored needs to be annotated with `@Persistent`.

There are some restrictions on the data objects in Java. They’re mostly requirements to keep the tangle of object pointers manageable:

- When a persistent object contains another persistent object as a field, it owns that object, and no other persistent object is allowed to have a reference to the owned object. This means that we sometimes need to save objects.
- When a persistent object contains a collection of other persistent objects, it owns all of the objects in the collection.
- We’re limited to the basic Java collection classes. We can’t use arrays, and we can’t use any of the extended collection types. We can use concrete classes like ArrayList, LinkedList, HashSet, TreeSet, Stack, and Vector. We can also use the more abstract interfaces, like List, but when we save and then reload an object, we can’t guarantee that the type of list will be the same in the restored
