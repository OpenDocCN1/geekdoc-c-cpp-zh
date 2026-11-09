Once I have the handler, I tell App Engine that it should route messages received at the email URL to the script containing that handler by adding an entry to app.yaml:

```
- url: /_ah/mail/.+
  script: chatmail.py
```

The InboundEmailMessage contains fields for all of the headers and body elements of an email message:

+   - **sender**: The email address of the message sender.
+   - **to**: The email addresses to in the To: header.
+   - **cc**: The email addresses in the cc: header.
+   - **reply_to**: The email address that replies should be sent to, as specified by the Reply-To: header.
+   - **subject**: The value of the message subject.
+   - **body**: The content of the message body.
+   - **attachments**: A list of attachments from the message. This is a list of pairs, where the first element is the attachment name and the second is the contents of the attachment.

# 15.5 Wrapping Up Services

In this chapter, we took a quick look at the idea of services in App Engine. We’ve seen a collection of the most common App Engine services, including services for providing high-speed access to commonly used data objects and for doing HTTP requests to communicate with other web services, as well as some basic communication services for sending and receiving email and chat messages. In the process, we saw what services look like and how we can interact with them. We saw how App Engine allows us to implement handlers for incoming data, even when it isn’t really HTTP by using pseudo-URLs and HTTP facades. And we used a couple of services to enhance the applications we built before. We used Memcache to provide caching for the filesystem we’ve been working on, and we used the email service to allow our chat application to receive email from its users.