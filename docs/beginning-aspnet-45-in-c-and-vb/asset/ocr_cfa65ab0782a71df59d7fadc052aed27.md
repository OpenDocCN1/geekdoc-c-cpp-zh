VB.NET

```
Imports System.Net.Mail
```

C#

```
using System.Net.Mail;
```

3. Add the following code to a Page_Load handler. If you're using VB.NET, you need to set up the handler first using the two drop-down lists at the top of the Document Window (or by double-clicking the page in Design View):

```
VB.NET
Protected Sub Page_Load(sender As Object, e As EventArgs) Handles Me.Load
    Dim myMessage As MailMessage = New MailMessage()
    myMessage.Subject = "Test Message"
    myMessage.Body = "Hello world, from Planet Wrox"
    myMessage.From = New MailAddress("you@example.com", "Sender Name")
    myMessage.To.Add(New MailAddress("you@example.com", "Receiver Name"))

    Dim mySmtpClient As SmtpClient = New SmtpClient()
    mySmtpClient.Send(myMessage)
End Sub
```

```
C#
protected void Page_Load(object sender, EventArgs e)
{
    MailMessage myMessage = new MailMessage();
    myMessage.Subject = "Test Message";
    myMessage.Body = "Hello world, from Planet Wrox";
    myMessage.From = new MailAddress("you@example.com", "Sender Name");
    myMessage.To.Add(new MailAddress("you@example.com", "Receiver Name"));

    SmtpClient mySmtpClient = new SmtpClient();
    mySmtpClient.Send(myMessage);
}
```

Change the e-mail addresses and names in the two lines that set the From and To addresses to your own. If you have only one e-mail address, you can use the same address for the sender and the receiver.

4. Open Web.config and right before the closing </configuration> tag, add the following settings:

```
<system.net>
  <mailSettings>
    <smtp deliveryMethod="Network" from="Your Name &lt;you@example.com&gt;">
      <network host="smtp.example.com" />
    </smtp>
  </mailSettings>
</system.net>
</configuration>
```

Don't forget to change smtp.example.com to the name of your SMTP server. Also, be sure to enter your name and e-mail address in the from attribute. If necessary, add the userName, password, enableSsl, and port attributes to the <network> element as shown earlier.