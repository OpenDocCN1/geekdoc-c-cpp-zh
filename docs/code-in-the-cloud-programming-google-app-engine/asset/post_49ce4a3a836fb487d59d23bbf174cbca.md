
```java
msgList = new ChatMessageList(chat, System.currentTimeMillis());
}
for (PChatMessage msg : messages) {
    msgList.addMessage(msg.asChatMessage());
}
return msgList;
} finally {
    persister.close();
}
}
```

This is almost the same as the updated getMessages, except for two changes to the JDOQL query:

- 1. We added a new parameter to the query, so that we can compare the date passed to the call to getMessagesSince with the dates on the messages.
- 2. We added a new clause to the query to compare the dates.

### 12.3 Updating the Client

Now we’ve got all of the server methods we need for interacting with our client! Our application is very nearly ready to run. What we still need to do is make a couple of changes to our client so that it knows how to use our updated RPC interfaces.

There’s not much to do here: basically, the only problem is that we need to update our code to adapt to the changes we made in the RPC service. Instead of getting a list of chat messages, it now gets a ChatMessageList, and now whenever it receives a ChatMessageList, it needs to update its stored last message time so that the client can use it to make incremental update requests. All we need to do for that is update our addNewMessages method:

```java
protected void addNewMessages(ChatMessageList newMessages) {
    lastMessageTime = newMessages.getTimestamp();
    StringBuilder content = new StringBuilder();
    content.append(text.getText());
    for (ChatMessage cm : newMessages.getMessages()) {
        content.append(renderChatMessage(cm));
    }
    text.setText(content.toString());
}
```

And then, we also need to update the code that creates a timed update so that it uses the lastMessageTime in its incremental update request:

```java
// Create a new message
Timer elapsedTimer = new Timer() {
    public void run() {
        chatService.getMessagesSince(getCurrentChat(), lastMessageTime,
                new MessageListCallback());
    }
};
// Schedule the timer for every 1/2 second (500 milliseconds)
elapsedTimer.scheduleRepeating(500);
```

### 12.4 Chat Administration

There’s one last thing to do before we’re ready to run our chat application. We provided a method for creating chats on the server, but we don’t have any interface for doing it. For now, we’re not going to build a new UI element for adding chats. Instead, we’ll write a bit of administration code. Administration code is code that you write to set up, clean up, initialize, or monitor things. It’s code that’s not there for our users to access but for us to use to manage our system.

A lot of times, you’ll build a UI for your administration code. For example, if you wanted to be able to keep track of how many people were accessing chat, how many messages they posted to which chat rooms, and how frequently people accessed the system, you’d probably want to have a UI. Then you’d build another GWT user interface for doing administration; to administer things, you’d just load the URL for the administrator’s UI in your browser. If you did that, you’d probably want to be careful to provide some security mechanisms, which we’ll see later, to make sure that only you could access the administration UI. But there are other kinds of administration code, which is what we’re interested in here. When we first deploy a server, we need to initialize some things. In our chat application, we need to initialize the set of chat rooms.

The problem is we can’t just run code on the server to set things up. We’re limited to the interface provided by App Engine. What we need to do is *self-detecting initialization*. That is, we need to put code in to detect when the server is not yet initialized and call the initialization method.

We do that by modifying getChats. Every time users come to our application but before they see anything else, the application will call getChats to initialize the chat list view. So what we'll do is simple. When the application retrieves the list of chat rooms, we'll have it check to see if the result is empty. If it is, we'll call a method to initialize a set of chat rooms. We'll put the initialization method in the server implementation, but we won't declare it as an RPC. We don't want users to be able to invoke it: the only way it should ever be invoked is by the automatic invocation when the system detects that it hasn't been initialized.

The code to initialize the chat is pretty simple. We create a PersistenceManager, create the rooms, and make them persistent:

Download workspace/Chat/src/com/pragprog/ebook/chat/server/ChatServiceImpl.java

```java
static final String[] DEFAULT_ROOMS =
    new String[] { "chat", "book", "java", "python" };

public List<ChatRoom> initializeChats(PersistenceManager persister) {
    List<ChatRoom> rooms = new ArrayList<ChatRoom>();
    List<PChatRoom> prooms = new ArrayList<PChatRoom>();
    long now = System.currentTimeMillis();
    for (String name : DEFAULT_ROOMS) {
        PChatRoom r = new PChatRoom(name, now);
        prooms.add(r);
        rooms.add(r.asChatRoom());
        persister.makePersistent(r);
    }
    return rooms;
}
```

To call it, we just add a test to getChats, which checks to see if the list of chats in the datastore is empty. If it is, we make it call initializeChats.

Download workspace/Chat/src/com/pragprog/ebook/chat/server/ChatServiceImpl.java

```java
@SuppressWarnings("unchecked")
public List<ChatRoom> getChats() {
    PersistenceManager persister = Persister.getPersistenceManager();
    try {
        Query query = persister.newQuery(PChatRoom.class);
        query.setOrdering("date");
        List<PChatRoom> rooms = (List<PChatRoom>)query.execute();
        if (rooms.isEmpty()) {
            return initializeChats(persister);
        } else {
            List<ChatRoom> result = new ArrayList<ChatRoom>();
            for (PChatRoom pchatroom : rooms) {
                result.add(pchatroom.asChatRoom());
            }
            return result;
        }
    } finally {
        persister.close();
    }
}
```

### 12.5 Running and Deploying the Chat Application

We’ve finally finished a Java version of the chat room! Now it’s time to test it. In Eclipse, you just run your application using the Run button. It takes a few moments to start up, and then it will show you a URL to use to access the test server. When you go to that URL, you’ll be asked to install a browser plugin: for testing purposes, it uses a special mechanism to manage communication between the client and the server so that you can use the Eclipse debugger to trace things in both the client and the server. (In fact, it will even let you trace an RPC call from the point where it’s invoked on the client to where it’s actually executed on the server.) Eclipse makes debugging an App Engine program nearly as simple as a traditional application.

Before you can deploy your Java code to the App Engine servers, you need to do a complete GWT compile. As usual, Eclipse makes things easy. First, you need to do a full GWT compile. Normally, Eclipse is doing partial compilation—basically just using the Java compiler in a restricted mode. To deploy, you need to do a full compile with full translation of Java to JavaScript. Up on the Eclipse toolbar, there’s a button that looks like a red toolbox with a Google G: just click on that, and Eclipse will do a full-blown GWT compilation.

And now, finally, our application is ready to go live! Right next to the toolbar button that you used to compile the application, there’s a button that looks like the App Engine jet-engine logo. Just click on that. The first time you do that, it will prompt you for the App Engine application ID, and then it will do the deployment. It takes a few minutes to do a full deployment, but once it’s done, your application is live on App Engine.

So, after all of this work, what does it look like? Cast your eyes over Figure 12.1, on the following page.

Pretty sharp, eh?

Just like with the Python applications, you now have full access to all of the administrative controls on the application dashboard.
