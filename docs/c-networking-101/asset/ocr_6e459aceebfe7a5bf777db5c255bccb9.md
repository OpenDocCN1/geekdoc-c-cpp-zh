```
```cpp
vmime::shared_ptr tr = sess->getTransport("smtp",
"smtp.example.com");

// Connect to server

tr->connect();

// Send the message

tr->send(msg);

// Disconnect

tr->disconnect();

return 0;

}
```
```

This program teaches you to send an email using VMime.

# Receive Emails using VMime

And now, let us see a simple example of how to receive emails with
VMime:

```
```cpp
#include
```
```