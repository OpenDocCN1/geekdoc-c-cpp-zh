We turn it into an asynchronous interface as usual:

```
```java
package com.pragprog.aebook.persistchat.client;

import java.util.Date;
import java.util.List;

import com.pragprog.aebook.persistchat.ChatMessage;
import com.google.gwt.user.client.rpc.AsyncCallback;

public interface ChatSubmissionServiceAsync {
    void postMessage(ChatMessage message,
        AsyncCallback<List<ChatMessage>> callback);

    void getMessages(String chatroom,
        AsyncCallback<List<ChatMessage>> callback);

    void getMessagesSince(String chat, Date timestamp,
        AsyncCallback<List<ChatMessage>> callback);
}
```
```

We implement that with a class in the server package. The implementation is very straightforward. We use the Persister that we just implemented to get a PersistenceManager for the operation, to make the message object persistent so that it will be saved as part of a transaction, and then to close the persistence manager, which will execute the transaction. Finally, we use the other service method, invoked directly from the server, to provide the user with an updated list of the messages in the chat.

```
```java
public List<ChatMessage> postMessage(ChatMessage message) {
    PersistenceManager persister = Persister.getPersistenceManager();
    persister.makePersistent(message);
    persister.close();
    return getMessages(message.getChat());
}
```
```

If we want to save any other objects as part of the same transaction as the chat message, we just add more calls to makePersistent to store them before the call to close.