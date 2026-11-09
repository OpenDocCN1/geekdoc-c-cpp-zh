
```java
// Check if I'm logged in.
if (xmpp.getPresence(jid).isAvailable()) {
  // send the message
  SendResponse status = xmpp.sendMessage(msg);
  if (status.getStatusMap().get(jid) != SendResponse.Status.SUCCESS) {
  }
}
}
}
```

As usual, the Java is a bit more complicated: you need to create an identifier object for the user instead of just directly passing a string. But once again it’s just boilerplate: write it once, and then reuse it.

## Receiving Instant Messages

Receiving messages from XMPP is a bit harder than sending, but it’s still pretty straightforward. As far as your App Engine code is concerned, XMPP is nothing but a stylized way of using HTTP. With the App Engine webhooks facade, it appears as if it’s all implemented on top of HTTP in terms of POST to send a message. You don’t need to worry about how XMPP really works: App Engine takes care of that for you. All you need to worry about is how to handle the HTTP request sent to you by App Engine. So to set up your application to receive XMPP messages from the XMPP service, you need to do three things:

- 1. Tell App Engine that you want to receive XMPP messages. You do that by putting an entry in your application configuration file—that’s web.xml in Python or appengine-web.xml in Java.
- 2. Write an XMPP handler, which is really just a standard HTTP request handler that implements POST.
- 3. Register your XMPP handler. App Engine will always map XMPP messages to a specific URL: /_ah/xmpp/message/chat/, so you need to register the XMPP handler as the handler for that URL.

With that set up, people can send chat messages to your application by sending a message to anything@your-app-id.appspot.com.

## Handling Chat Messages in Python

In order to receive an XMPP message in Python, you first need to put the following entry into app.yaml:

```yaml
inbound_services:
- xmpp_message
```

Then write an XMPP handler:

```python
class XMPPHandler(webapp.RequestHandler):
    def post(self):
        message = xmpp.Message(self.request.POST)
        message.reply("Received message: %s\nHello to you too" % message.body)
```

You just take the POST request, have the XMPP service convert it to an XMPP message object, and then get the message (message.body), the sender (message.sender), or the intended recipient (message.to).

Finally, you need to register that handler:

```python
application = webapp.WSGIApplication([('/_ah/xmpp/message/chat/', XMPPHandler)])
```

## Receiving Chat Messages in Java

The basic steps in Java are pretty much the same as Python, but as usual, it’s slightly different stylistically to match the differences between the languages. First, you tell App Engine that you want to receive chat messages by adding an entry to the application configuration in appengine-web.xml.

```xml
<inbound-services>
    <service>xmpp_message</service>
</inbound-services>
```

Then, write a message handler:

```java
import java.io.IOException;
import javax.servlet.http.*;
import com.google.appengine.api.xmpp.JID;
import com.google.appengine.api.xmpp.Message;
import com.google.appengine.api.xmpp.XMPPService;
import com.google.appengine.api.xmpp.XMPPServiceFactory;

public class XMPPReceiverServlet extends HttpServlet {
    public void doPost(HttpServletRequest req, HttpServletResponse res)
            throws IOException {
        XMPPService xmpp = XMPPServiceFactory.getXMPPService();
        Message message = xmpp.parseMessage(req);

        JID fromJid = message.getFromJid();
        String body = message.getBody();
        // ...
    }
}
```

And finally, register this handler by adding servlet and servlet-mapping entries to your web.xml file, as shown in the following configuration:

An implementation of that. The Java code equivalent to the simple one-line Python script above is this:

```java
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
    Message msg = new MimeMessage(mailSession);
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

## Receiving Mail

Receiving mail is a bit more complicated, but not by much. It follows the usual App Engine pattern for receiving data via a service. You tell App Engine that you want to receive data from the service by putting an entry into the application configuration. Then App Engine will route incoming messages from that service via a virtual HTTP URL, where it can be handled by your message handler/servlet. In the interests of simplicity, I'll show you a quick example of how a Python application can receive email; Java is, as usual, pretty much the same but a bit more verbose.

Step one of the pattern is telling App Engine that your application wants to receive incoming email using the email service. To do that, you just add an inbound_services entry to your app.yaml file:

```yaml
inbound_services:
- mail
```

Once you’ve set that up, your application is ready to receive email. You’ll get any email addressed to a username at your-app-id.appspotmail.com. You’ll need to set up a handler for incoming email. Email will be received at the virtual URL /_ah/mail/receiver-address. So, for example, if someone sends mail to admin@markcc-chatroom-one.appspot.com, my application would receive that email on the URL /_ah/mail/admin@markcc-chatroom-one.appspot.com.

In order to handle the email, you need to set up a handler for the email URLs. Suppose that I wanted to add an email capability to the chat service so that people could send email to the admin address, and that mail would be automatically forwarded to me. What I would need to do is add a script for handling the incoming email. Since it’s being disguised as an HTTP request, if I were to implement it as just a simple RequestHandler, I would need to parse the incoming request into a mail message. But instead of making me do that manually, App Engine provides a InboundMailHandler class that I can inherit from. It provides an implementation of post that takes the incoming message, parses it into a InboundEmailMessage, and then invokes receive on the message. So all I need to do is provide an implementation of receive, such as the following:

```python
import email
from google.appengine.ext import webapp
from google.appengine.ext.webapp.mail_handlers import InboundMailHandler
from google.appengine.ext.webapp.util import run_wsgi_app

class ChatMailHandler(InboundMailHandler):
    def receive(self, mail_message):
        mail.send_mail(sender="admin@markcc-chatroom-one.appspot.com",
                       to="markcc@gmail.com",
                       subject="CHAT ADMIN MAIL: %s" % mail_message.subject,
                       body="Original message from: %s\n%s" %
                            (mail_message.sender,
                             mail_message.body))

chatmail = webapp.WSGIApplication([InboundMailHandler.mapping()])

def main():
    run_wsgi_app(chatmail)

if __name__ == "__main__":
    main()
```

Once I have the handler, I tell App Engine that it should route messages received at the email URL to the script containing that handler by adding an entry to app.yaml:

```yaml
- url: /_ah/mail/.+
  script: chatmail.py
```

The InboundEmailMessage contains fields for all of the headers and body elements of an email message:

- **sender**: The email address of the message sender.
- **to**: The email addresses to in the To: header.
- **cc**: The email addresses in the cc: header.
- **reply_to**: The email address that replies should be sent to, as specified by the Reply-To: header.
- **subject**: The value of the message subject.
- **body**: The content of the message body.
- **attachments**: A list of attachments from the message. This is a list of pairs, where the first element is the attachment name and the second is the contents of the attachment.

## 15.5 Wrapping Up Services

In this chapter, we took a quick look at the idea of services in App Engine. We’ve seen a collection of the most common App Engine services, including services for providing high-speed access to commonly used data objects and for doing HTTP requests to communicate with other web services, as well as some basic communication services for sending and receiving email and chat messages. In the process, we saw what services look like and how we can interact with them. We saw how App Engine allows us to implement handlers for incoming data, even when it isn’t really HTTP by using pseudo-URLs and HTTP facades. And we used a couple of services to enhance the applications we built before. We used Memcache to provide caching for the filesystem we’ve been working on, and we used the email service to allow our chat application to receive email from its users.
