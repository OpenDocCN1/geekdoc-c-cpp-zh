Then write an XMPP handler:

```
class XMPPHandler(webapp.RequestHandler):
    def post(self):
        message = xmpp.Message(self.request.POST)
        message.reply("Received message: %s\nHello to you too" % message.body)
```

You just take the POST request, have the XMPP service convert it to an XMPP message object, and then get the message (message.body), the sender (message.sender), or the intended recipient (message.to).

Finally, you need to register that handler:

```
application = webapp.WSGIApplication([('/_ah/xmpp/message/chat/', XMPPHandler)])
```

# Receiving Chat Messages in Java

The basic steps in Java are pretty much the same as Python, but as usual, it’s slightly different stylistically to match the differences between the languages. First, you tell App Engine that you want to receive chat messages by adding an entry to the application configuration in appengine-web.xml.

```
<inbound-services>
    <service>xmpp_message</service>
</inbound-services>
```

Then, write a message handler:

```
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