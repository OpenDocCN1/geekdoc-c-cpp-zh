We start with an Email class:

```
Download Ethernet/Email/email.h

#ifndef __EMAIL__H__
#define __EMAIL__H__

class Email {
    String _from, _to, _subject, _body;

public:

    Email(
        const String& from,
        const String& to,
        const String& subject,
        const String& body
    ) : _from(from), _to(to), _subject(subject), _body(body) {}

    const String& getFrom()    const { return _from; }
    const String& getTo()      const { return _to; }
    const String& getSubject() const { return _subject; }
    const String& getBody()    const { return _body; }
};

#endif
```

This class encapsulates an email's four most important attributes—the email addresses of the sender and the recipient, a subject, and a message body. We store all attributes as String objects.

Wait a minute...a String class? Yes! Since version 19, the Arduino IDE comes with a full-blown string class.¹⁴ It does not have as many features as the C++ or Java string classes, but it's still way better than messing around with char pointers. You'll see how to use it in a few paragraphs.

The rest of our Email class is pretty straightforward. In the constructor, we initialize all instance variables, and we have methods for getting every single attribute. We now need an SmtpService class for sending Email objects:

```
Download Ethernet/Email/smtp_service.h

Line 1  #ifndef __SMTP_SERVICE__H__
        #define __SMTP_SERVICE__H__
        
        #include "email.h"
```

14. http://arduino.cc/en/Reference/StringObject