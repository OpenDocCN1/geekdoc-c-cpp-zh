an implementation of that. The Java code equivalent to the simple one-line Python script above is this:

```
import java.util.Properties;

import javax.mail.Message;
import javax.mail.MessagingException;
import javax.mail.Session;
import javax.mail.Transport;
import javax.mail.internet.AddressException;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;

...

Session mailSession = Session.getDefaultInstance(new Properties(), null);
try {
    Message msg = new MimeMessage(session);
    msg.setFrom(new InternetAddress("chat-service@markcc-java-chat.appspot.com"));
    msg.addRecipient(Message.RecipientType.TO,
        new InternetAddress("markcc@gmail.com"));
    msg.setSubject("Hi Mark!");
    msg.setText("I'm still running!");
    Transport.send(msg);
} catch (AddressException e) {
    // what to do if the address was invalid
} catch (MessagingException e) {
    // what to do if there was an error sending it other than
    // a bad email address
}
```

# Receiving Mail

Receiving mail is a bit more complicated, but not by much. It follows the usual App Engine pattern for receiving data via a service. You tell App Engine that you want to receive data from the service by putting an entry into the application configuration. Then App Engine will route incoming messages from that service via a virtual HTTP URL, where it can be handled by your message handler/servlet. In the interests of simplicity, I'll show you a quick example of how a Python application can receive email; Java is, as usual, pretty much the same but a bit more verbose.

Step one of the pattern is telling App Engine that your application wants to receive incoming email using the email service. To do that, you just add an inbound_services entry to your app.yaml file:

```
inbound_services:
- mail
```