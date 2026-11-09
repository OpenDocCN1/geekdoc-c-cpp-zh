to initialize the chat list view. So what we'll do is simple. When the application retrieves the list of chat rooms, we'll have it check to see if the result is empty. If it is, we'll call a method to initialize a set of chat rooms. We'll put the initialization method in the server implementation, but we won't declare it as an RPC. We don't want users to be able to invoke it: the only way it should ever be invoked is by the automatic invocation when the system detects that it hasn't been initialized.

The code to initialize the chat is pretty simple. We create a PersistenceManager, create the rooms, and make them persistent:

Download workspace/Chat/src/com/pragprog/ebook/chat/server/ChatServiceImpl.java

```
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
```

To call it, we just add a test to getChats, which checks to see if the list of chats in the datastore is empty. If it is, we make it call initializeChats.

Download workspace/Chat/src/com/pragprog/ebook/chat/server/ChatServiceImpl.java

```
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
    }
}
```
```