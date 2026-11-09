```
PChatRoom chat = chats.get(0);
chat.updateLastMessageDate(timestamp);
} finally {
    persister.close();
}
```

We start off with some typical App Engine boilerplate: create a PersistenceManager, and make the chat message object persistent so that it will be stored in the datastore. Then we get to the new stuff.

+   1. We modify the date on the message. As I explained before, we have to be very careful to only use one clock—App Engine’s clock. We don’t care what the client thought the date and time was; we need to use the date here on the server.
+   
+   2. Our Chat objects must include the timestamp of the last posted message. So we need to retrieve the chat object in order to update its last-message time to the time of this message.
+   
+   3. The query returns a list of chats, but we know that the list will only have one entry, so we can just grab the only entry out of the list.
+   
+   4. Now we update the last message date in the chat object. We don’t need to do anything to store it, since we retrieved the message using a PersistenceManager query, it’s already managed by the PersistenceManager. And that means the updates will automatically be saved at the end of the transaction.

Finally, we need the incremental getMessagesSince:

Download workspace/Chat/src/com/pragprog/ebook/chat/server/ChatServiceImpl.java

```
@SuppressWarnings("unchecked")
public ChatMessageList getMessagesSince(String chat, long timestamp) {
    PersistenceManager persister = Persister.getPersistenceManager();
    try {
        Query query = persister.newQuery(PChatMessage.class);
        query.declareParameters("String desiredRoom, int earliest");
        query.setFilter("chat == desiredRoom && date > earliest");
        query.setOrdering("date");
        List<PChatMessage> messages =
            (List<PChatMessage>)query.execute(chat, timestamp);
        ChatMessageList msgList = null;
        // Get the most recent message.
        if (messages.size() >= 1) {
            PChatMessage lastMessage = messages.get(messages.size() - 1);
            msgList = new ChatMessageList(chat, lastMessage.getDate());
        } else {
```