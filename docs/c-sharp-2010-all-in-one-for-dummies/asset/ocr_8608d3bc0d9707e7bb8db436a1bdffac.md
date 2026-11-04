If you are in a corporate environment, however, you can usually talk to your e-mail administrator and get permission to use the e-mail server. Because outgoing requests are usually only harnessed inside the firewall, relaying is often available. To build your e-mail function, follow these steps:

+   1. **Add a text box to the default form in Design View, and then change to Code View.**
+      At the top of Code View, make sure that you have referenced the `System.Net.Mail` namespace.
+   2. **Create a new subroutine called SendEmail.**
+      It should accept the from e-mail address, the to e-mail address, the subject of the e-mail, and the body of the e-mail.
+   3. **Declare a new MailMessage and pass in the fromAddress, toAddress, subject, and body parameters, like this:**
+      `MailMessage message = New MailMessage(fromAddress, toAddress, subject, body);`
+   4. **Declare a new SmtpClient and pass in the address of your mail server.**
+      This can be an IP address, machine name, or URL.
+   5. **Use the Send method of the SmtpClient object you created to send the MailMessage, which is passed in as a parameter.**
+   6. **When you're finished, make sure that you set the values of the MailMessage and SmtpClient to Nothing, because they do take up resources.**

Listing 4-2 shows the completed subroutine.

# Listing 4-2: The SendEmail Subroutine

```
private void SendEmail(string fromAddress, string toAddress, string subject,
    string body)
{
    MailMessage message = new MailMessage(fromAddress, toAddress, subject, body);
    SmtpClient mailClient = new SmtpClient("localhost");
    mailClient.Send(message);
    message = null;
    mailClient = null;
}
```

Note that I used localhost as the e-mail server name. If you have an e-mail server software installed locally, even IIS 6.0 with SMTP, this will work. Most of the time, you will have to put another e-mail server name in the SmtpClient constructor. The e-mail server name can often be found in your Outlook preferences.