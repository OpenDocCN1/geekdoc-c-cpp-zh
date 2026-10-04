
# Using the System.Net Namespace 463

- 6. Set the Method parameter of the FtpWebRequest to WebRequestMethods.Ftp.DownloadFile.
- 7. Set the Credentials property of the FtpWebRequest to a new NetworkCredential with anonymous information, like I did in Listing 4-1.
- 8. Create a new WebResponse object from the FtpRequest method. This gets the state back from the FTP server as how your request will be handled.
- 9. Get the Stream from the Response object.
- 10. Read the file in a 1024-byte buffer, one block at a time, using While, as shown at the end of Listing 4-1.
- 11. Call the DownloadFile method from the Button1_Click event handler, like this in this chunk of code:

```csharp
private void buttonClick(object sender, EventArgs e)
{
    DownloadFile("http://ftp.fsharpordummies.net/sampleFile.bmp", "c:\sampleFile.bmp");
}
```

This FTP is watered down, but it makes my point. The HttpRequest and Response classes in the System.Net namespace are fully utilized to create the more complete FtpWebRequest, for instance. Properties like Method of download and Credentials make it an easy call.

In fact, the toughest part of this process is dealing with a FileStream object, which is still the best way to move files and not specific to the System.Net namespace. Streams are discussed in Chapter 3 of this minib, covers the System.IO namespace, but they have significance to the network classes too. Streams represent a flow of data of some kind, and a flow of information from the Internet qualifies.

That's what you are doing when you get a web page or a file from the Internet — getting a flow of data. If you think about it, it makes sense that this is a flow, the status bar in an application shows a percentage of completion. Like pouring water into a glass, the flow of data is a stream, so the concept is meant Stream.

This concept holds true for getting a file from the Wide Web, as well. HTTP, the web protocol, is just another protocol that defines how a document is transferred from a server on the Internet to your local machine. In fact, the code looks strikingly similar to the FTP example, as you see in the little bit of code. The same stream is recovered; only the formatting is different.

| Book III Accessing the Internet |
| :--- |
| Chapter 4 |

# 464 Using the System.Net Namespace

```csharp
private void DownloadWebFile(string remoteFile, string localFile)
{
    FileStream localFileStream = new FileStream(localFile, FileMode.OpenOrCreate);
    WebRequest request = WebRequest.Create(remoteFile);
    request.Method = WebRequestMethods.Http.Get;
    WebResponse response = request.GetResponse();
    Stream responseStream = response.GetResponseStream();
    byte[] buffer = new byte[1024];
    int bytesRead = responseStream.Read(buffer, 0, 1024);
    while (bytesRead > 0)
    {
        localFileStream.Write(buffer, 0, bytesRead);
        bytesRead = responseStream.Read(buffer, 0, 1024);
    }
    localFileStream.Close();
    responseStream.Close();
}
```

You need to pass a web address, so your subroutine call looks like this:

```csharp
DownloadWebFile("http://your.server.com/sampleFile.bmp", "C:\sampleFile.bmp");
```

Note the changes, marked as bold. WebRequest is now a WebRequest rather than an FtpWebWebRequest. Also, the Method property of webRequest has been changed to WebRequestMethods.Http.Get. Finally, the Credentials property has been removed because the credentials are no longer required.

# E-mailing a status report

E-mail is a common requirement of networked systems. If you are working in an enterprise environment, you are going to write a larger scale application to handle all e-mail requirements, rather than make individual application e-mail.

However, if you are writing a stand-alone product, it might require e-mail support. Because I have to be writing a stand-alone application, that is exactly what I'm going to do.

E-mail is a server-based operation, so if you don't have an e-mail server that you can use to send from, this might be hard. Many ISPs no longer allow relaying, which is sending an outgoing message without first having an account and logging in. Therefore, you might have trouble testing this part of the sample.

If you are in a corporate environment, however, you can usually talk to your e-mail administrator and get permission to use the e-mail server. Because outgoing requests are usually harnessed inside the firewall, relaying is often available. To build your e-mail function, follow these steps:

![](img/6df7bb88e9302e98442acc219cfbd7fc_489_0.png)

# Using the System.Net Namespace 465

- 1. Add a text box to the default form in Design View and change to Code View.

At the top of Code View, make sure that you have referenced the System.Mail namespace.

- 2. Create a new subroutine called SendEmail.

It should accept the e-mail address, the subject of the email, and the body of the e-mail.

- 3. Declare a new MailMessage and pass in the fromAddress, to-address, and body parameters, like this:

```csharp
MailMessage message = new MailMessage(fromAddress, toAddress, body);
```

- 4. Declare a new SmtClient and pass in the address of your mail

This can be an IP address, machine name, or URL.

- 5. Use the Send method of the SmtClient object to create sent MailMessage, which is passed in as a parameter.

- 6. When you're finished, make sure that you set the values of the MailMessage and SmtpClient to Nothing, because they do not release resources.

Listing 4-2 shows the completed subroutine.

# Listing 4-2: The SendEmail Subroutine

```csharp
private void SendEmail(string fromAddress, string toAddress, string body)
{
    MailMessage message = new MailMessage(fromAddress, toAddress, body);
    SmtpClient client = new SmtpClient("localhost");
    client.Send(message);
    message = null;
    client = null;
}
```

Notice I used localhost as the e-mail server name. If you have e-mail installed locally, with IIS 6.0 this will work. The e-mail server name is often found in your preferences.

After you have written your method, you need to call it in the Button_Click event handler. Change the code of that to the following:

# 466 Using the System.Net Namespace

```csharp
private void button1_Click(object sender, EventArgs e)
{
    DownloadFile("ftp://ftp.fsharpordummies.net/sampleFile.bmp", "c:\sampleFile.bmp");
    SendEmail(textBox1.Text, textBox2.Text, "FTP Successfully downloaded");
}
```
