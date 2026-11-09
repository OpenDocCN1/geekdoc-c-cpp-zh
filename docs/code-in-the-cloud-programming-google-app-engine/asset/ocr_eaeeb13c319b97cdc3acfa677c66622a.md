```
```java
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
```