We put the RPC version of the ChatMessage and ChatRoom classes in the client package, and we put the persistent version of them into the server package. To make things easier to read, we prefix the names of the persistent version of classes with P; you’ll see why later, where we need to do the work to convert between the two different versions.

For now, so that you can see the difference, let’s look at the persistent version of our new ChatRoom. We just saw the RPC version of it, and here’s the datastore persistent ChatRoom.

```
Download workspace/Chat/src/com/pragprog/ebook/chat/server/PChatRoom.java

@PersistenceCapable(identityType = IdentityType.APPLICATION)
public class PChatRoom {
    @PrimaryKey
    @Persistent(valueStrategy = IdGeneratorStrategy.IDENTITY)
    private Key key;

    @Persistent
    String name;

    @Persistent
    long date;

    public PChatRoom() {
    }

    public PChatRoom(String chat, long date) {
        this.date = date;
        this.name = chat;
    }

    public ChatRoom asChatRoom() {
        return new ChatRoom(name, date);
    }

    public String getName() {
        return name;
    }

    public Key getKey() {
        return key;
    }

    public long getLastMessageDate() {
        return date;
    }

    public void updateLastMessageDate(long d) {
        date = d;
    }
}
```