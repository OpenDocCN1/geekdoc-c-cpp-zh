
## How to send email

When you create a web application, you often need to send email messages from the application. For instance, when a user makes a purchase from an ecommerce site, a web application usually sends an email to the customer that confirms the order. Or, if a serious error occurs, the web application often sends an email message to the support staff that documents the error. In the topics that follow, you’ll learn how to send email from your ASP.NET applications.

## An introduction to email

You’re probably familiar with *mail client* software such as Microsoft Outlook or Outlook Express that allows you to send and retrieve email messages. This type of software communicates with a *mail server* that actually sends and retrieves your email messages. Most likely, your mail server software is provided by your Internet Service Provider (ISP) or through your company.

The diagram in figure 20-1 shows how this works. The two protocols that are commonly used to send email messages are *SMTP* and *POP*. When you send an email message, the message is first sent from the mail client software on your computer to your mail server using the SMTP protocol. Then, your mail server uses SMTP to send the mail to the recipient’s mail server. Finally, the recipient’s mail client uses the POP protocol to retrieve the mail from the recipient’s mail server.

A third protocol you should know about is *MIME*, which stands for *Multipurpose Internet Mail Extension*. Unlike SMTP or POP, MIME isn’t used to transfer email messages. Instead, it defines how the content of an email message and its attachments are formatted. In this chapter, you’ll learn how to send messages that consist of simple text as well as messages that use HTML format.

## How email works

![](img/c024ccf88e28c30c07dd410d4342288f_686_0.png)

## Three email protocols

| Protocol | Description |
|---|---|
| SMTP | *Simple Mail Transfer Protocol* is used to send a message from one mail server to another. |
| POP | *Post Office Protocol* is used by mail clients to retrieve messages from mail servers. POP version 3, known as POP3, is the most widely used version, but a specification for POP version 4 has been developed. |
| MIME | The *Multipurpose Internet Mail Extension* specifies the type of content that can be sent as a message or attachment. |

## Three common reasons for sending email from an ASP.NET application

- **To confirm receipt of an order.** When the user completes an order, the application can email a confirmation of the order to the user.
- **To remind a registered user of a forgotten password.** If the user forgets his or her password, the application can email the password to the email address that’s on file for the user. You can also accomplish this using the PasswordRecovery control presented in chapter 19.
- **To notify support personnel of a problem.** If a problem like an unhandled exception occurs, the application can email a message that summarizes the problem to the appropriate support person.

## Description

- When an email message is sent, it goes from the sender’s *mail client* to the sender’s *mail server* to the receiver’s mail server to the receiver’s mail client.
- *SMTP* and *POP* are the protocols that are commonly used for sending and retrieving email messages. *MIME* is the protocol for defining the format of an email message.

## How to install an SMTP server

If you’re using the Web Development Server to test your ASP.NET applications, they won’t be able to send email. As a result, before you can test an ASP.NET application that sends email messages, you must install IIS and use it to run your web applications. In addition, before you can test an ASP.NET application that sends email messages, you must install an SMTP server.

If you’re using Windows XP, you can use the SMTP server that’s built into IIS. If you’re using Windows 7 or Windows Vista, however, you should know that the version of IIS that comes with these operating systems doesn’t include an SMTP server. Because of that, you’ll need to get a separate SMTP server. Several servers can be downloaded for free from the Internet.

To start the SMTP service under Windows XP, you use the IIS Management Console as shown in figure 20-2. To display this program, open the Control Panel and then open Administrative Tools and double-click the Internet Information Services icon. Once you’ve opened the IIS Management Console, you can expand the tree to display the Default SMTP Virtual Server node. Then, you can start the SMTP service by selecting it in the tree and clicking the Start button in the toolbar.

Once you’ve started the SMTP service, you must configure it so that it allows your ASP.NET applications to send mail. To do that, you enable relaying for the local computer. This allows the mail server to accept mail from a specified computer and deliver it to the intended recipient. To configure the SMTP service to relay mail from the local computer, open the Relay Restrictions dialog box as described in this figure and add the localhost address (127.0.0.1) to the list of computers that the SMTP server will relay mail for.

## How to make sure SMTP is running on your local server

![](img/c024ccf88e28c30c07dd410d4342288f_688_0.png)

- 1. Open the Control Panel, double-click on Administrative Tools, and then double-click on Internet Information Services to open the IIS Management Console shown above.
- 2. Expand the tree to display your local computer’s IIS server and the services running under it.
- 3. Select the Default SMTP Virtual Server service.
- 4. If the SMTP service is not running, the Stop button (■) will be disabled. In that case, click the Start button (▶) to start the SMTP service.

## How to allow relaying for the local host

![](img/c024ccf88e28c30c07dd410d4342288f_688_1.png)

![](img/c024ccf88e28c30c07dd410d4342288f_688_2.png)

- 1. In the IIS Management Console, right-click the Default SMTP Virtual Server node and choose the Properties command.
- 2. Click the Access tab, then click the Relay button. This displays the Relay Restrictions dialog box shown above.
- 3. Click the Add button to display the Computer dialog box shown above. Then, select Single Computer, type 127.0.0.1 into the IP address field, click OK to close the Computer dialog box, and click OK again to close the Relay Restrictions dialog box.

## How to create an email message

Figure 20-3 shows the constructors and properties of the MailMessage class that you use to create email messages. It also shows the constructors of the MailAddress class. This class is used to create the addresses that are stored in the From, To, CC, and Bcc properties of a mail message.

The first example in this figure illustrates how you can use these classes to create a mail message that includes a carbon copy (cc). Here, all of the values needed to create the email message are passed to the method as arguments. Then, the first three statements of the method create MailAddress objects for the from, to, and cc addresses. Notice that the MailAddress object for the from address includes both an email address and a display name. When a display name is included, it’s displayed in the mail client’s email list instead of the email address.

The fourth statement in this method creates a MailMessage object using the to and from MailAddress objects. Then, the next two statements set the Subject and Body properties of the message. Finally, the last statement adds the cc MailAddress object to the collection of objects in the CC property.

The second example in this figure shows how to create the same email as in the first example without setting the display name for the sender. To do that, you simply create the MailMessage object using the from and to addresses and the subject and body. This example also illustrates how you can create a MailAddress object for the carbon copy and add it to the collection of objects using a single statement.

Although the examples in this figure create messages that will be sent to a single recipient, you should realize that you can send a message to any number of recipients. To do that, you need to use the first constructor for the MailMessage class shown here to create an empty mail message. Then, you can create a MailAddress object for the sender and assign it to the From property of the message. And you can create a MailAddress object for each recipient and add it to the collection of MailAddress objects returned by the To property of the mail message. For example, to create a message that will be sent to two people, your code will look something like this:

```
MailMessage msg = new MailMessage();
msg.From = new MailAddress("anne@murach.com");
msg.To.Add(new MailAddress("joel@murach.com"));
msg.To.Add(new MailAddress("kelly@murach.com"));
```
