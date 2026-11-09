```
```java
public long getTimestamp() {
    return time;
}

public void addMessage(ChatMessage msg) {
    messages.add(msg);
}

public void addMessages(List<ChatMessage> messages) {
    messages.addAll(messages);
}
```
```

# Making the Chat Interface Incremental

To start using this time-based incremental retrieval mechanism, we’ll need to both modify some old methods and add some new methods to our interface:

Download workspace/Chat/src/com/pragprog/ebook/chat/client/ChatService.java

```
```java
void postMessage(ChatMessage messages);
ChatMessageList getMessages(String room);
ChatMessageList getMessagesSince(String chat, long timestamp);
```
```

+   1. Our postMessage method originally returned the list of messages in a chat. But the reason we wanted to add a method to get the messages since a particular point in time (that is, that we don’t want to send the same old messages over and over again) applies just as well to the result of the postMessage method as it does to the result of getMessages. We have two choices: we can either add a timestamp parameter to postMessage, or we can make postMessage return no value and instead have our client call getMessages after a new message is posted.
+   
+      As a general rule, it’s good to separate query methods (methods that retrieve values) from update methods (methods that modify values). We’ll follow that rule and make postMessage have a void return value.
+   
+   2. When a user first connects to a chat room, the client should fetch all of the messages in that room. After that, it will start doing the incremental fetches. In order to make that work, the client needs to know the server time when they did their first fetch. We must modify the return type of the getMessages call so that it returns a ChatMessageList.
+   
+   3. Now we finally get to a new method: getMessagesSince.