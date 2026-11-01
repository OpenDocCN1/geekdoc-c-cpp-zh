hosting your site with an external hosting party, you need to use the SMTP server it provides. Contact your network administrator or your ISP if you are unsure about your SMTP server.

When you have the address of the SMTP server, you can configure it globally in the Web.config file in the <system.net> element. When you are using the SMTP server from your ISP, the configuration setting looks like this:

```
```xml
<system.net>
  <mailSettings>
    <smtp deliveryMethod="Network" from="Your Name &lt;you@example.com &gt;">
      <network host="smtp.example.com" />
    </smtp>
  </mailSettings>
</system.net>
...
</configuration>
```
```

You must add the <system.net> element as a direct child of the Web.config file's root element <configuration>. Within <system.net> you add a <mailSettings> element, which in turn contains an <smtp> element. Finally, the <network> element that points to your SMTP server.

The <smtp> element accepts an optional from attribute that enables you to set the name and e-mail address of the sender in the format Name <E-mail Address>. Because the angle brackets (< >) in XML have special meaning, you need to escape them with &lt; and &gt;. When you send e-mail programmatically, you can override this From address as you see in the next Try It Out exercise.

If your ISP requires you to authenticate before you can send the e-mail or wants you to use a different port number, you can add this information to the <network /> element:

```
```xml
<smtp deliveryMethod="Network" from="Your Name &lt;you@example.com &gt;">
  <network host="smtp.example.com" userName="UserName" password="Password"
    port="587" />
</smtp>
```
```

The port number varies from server to server. In some cases, you can leave out the port attribute and the SmtpClient will use the default port number (which is 25). Other port numbers that are frequently used include 465 and 587.

Some mail servers—like the one supplied by Gmail—require you to use Secure Sockets Layer (SSL), a technique that encrypts the data going to the mail server to improve security. In ASP.NET prior to version 4, you had to enable SSL programmatically in your own code. Fortunately, with the inclusion of the enableSsl attribute on the <network /> element, this is no longer the case. To use a Gmail server or any other mail server that requires SSL, you use a <network /> element that looks like this:

```
```xml
<network enableSsl="true" host="smtp.gmail.com" password="Password"
  userName="YourAccountName@gmail.com" port="587" />
```
```

Don't forget to enter your password and username—which in the case of Gmail is your full Gmail e-mail address. Depending on your settings, you may need to generate an application-specific password, which you can do here: http://bit.ly/N9Wv3S.