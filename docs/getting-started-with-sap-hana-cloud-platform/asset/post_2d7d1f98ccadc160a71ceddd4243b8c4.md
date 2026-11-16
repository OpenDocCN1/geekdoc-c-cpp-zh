
For simplicity's sake, we designed our sample application to fetch the API key at runtime from the Servlet context using the web.xml deployment descriptor file. For more information on how to set this up, look at the readme file in the source code bundle for this chapter and the comments in the web.xml file itself.

With your API key in hand, you essentially have everything you need to get started. Because you'll be using the Connectivity Service to broker the connection, you must create an HTTP destination to point to the API endpoint. Figure 6.40 shows the destination that we created. As you can see, we named the destination GoogleGeocodeDest and pointed it to the Geocoding API URL https://maps.googleapis.com/maps/api/geocode/json. Note that the Proxy Type is set to INTERNET, because this is to be an external call. If you were calling an API hosted on-premise, then you would have chosen the OnPREMISE option.

![](img/cf7012644082c115a2181376d9b7486d_275_0.png)

Figure 6.40 Creating an HTTP Destination for the Geocoding API

In this particular scenario, that's all the setup that's required. In more advanced scenarios, your job would be only slightly harder, in that you would likely have to configure more advanced authentication properties in order to support mutual authentication using certificates, OAuth/SAML assertions, and so on. Specific details for each of these authentication types are provided in the online help documentation.

## Calling the RESTful Service within a Java Application

With your HTTP destination in place, the steps required to set up the call to the Geocoding API service within your incident management application are as follows:

- 1. Define a resource reference to the HTTP destination within the application's web.xml file:

```
<web-app>
    ...
    <res-ref>
        <res-ref-name>GoogleGeocodeDest</res-ref-name>
        <res-type>com.sap.core.connectivity.api.http.HttpDestination
        </res-type>
        <res-auth>Application</res-auth>
    </res-ref>
</web-app>
```

- 2. Use a dependency injection to allocate the HttpDestination object at runtime:

```
public class IncidentBean
{
    @Resource(mappedName="GoogleGeocodeDest")
    private HttpDestination geocodeDestination;
    ...
}
```

- 3. Use the createHttpClient() instance method of the HttpDestination class to obtain a reference to an org.apache.http.client.HttpClient instance. From here on out, you can use this HTTP client connection to invoke the service just as you would outside of SAP HCP.

For brevity's sake, we won't include the detailed HTTP request handling logic in this section. However, if you're interested in seeing how this works, check out the loadGeoCoordinates() method of the com.sappress.hcbook.chp06.persistence.IncidentBean class. There, you can see how we're encoding the location address for transmission, parsing the JSON results, and storing the coordinate data inside of the Address entity object. You can test this feature from within the EDIT INCIDENT screen by clicking on the GET COORDINATES link, as shown in Figure 6.41.

![](img/cf7012644082c115a2181376d9b7486d_277_0.png)

Figure 6.41 Triggering the Geocoding API Call within the Incident Editor

## 6.3.5 Case Study: Sending an E-Mail Message

In our last case study, we'll demonstrate how the Connectivity Service can be used to send email messages. Here, you'll enhance your incident management application to include a link that allows users to send incident notification messages to interested parties as needed.

### Design Approach and Initial Setup

In many ways, the initial setup for this scenario mirrors the steps we demonstrated for the RESTful service call setup in Section 6.3.4. You basically need to collect the connection parameters for the mail server to which you wish to connect and then create a Mail destination to encapsulate these parameters. For the purposes of our demonstration, we'll be connecting to Google's Gmail server using the SMTP protocol.

![](img/cf7012644082c115a2181376d9b7486d_278_0.png)

Figure 6.42 Creating a Mail Destination in SAP HCP Cockpit

Whenever the destination is saved, the parameters are used to create a javax.mail.Session object that gets stored in the Java EE container's JNDI context under the mail/<Destination Name> context path (e.g., mail/Session in our example). In the next section, you'll see how your Java applications can pick up this object and use it to send email messages.

### Working with the javax.mail Library

Because the Connectivity Service takes the liberty of creating a javax.mail.Session object for us, the task of sending (or receiving) an email message is rather straightforward. The code excerpt contained in Listing 6.19 demonstrates this with a simple method called sendMessage() that can be used generically to send an email message to a particular recipient. The basic API call sequence is as follows:

- 1. First, the method creates a MimeMessage object that encapsulates the email message you'll be sending. This message instance is linked to the Session object that's loaded into context using the injection technique whenever the overarching EJB is instantiated.

- 2. Next, you bind the sender and receiver of the message and define the message subject line.

- 3. Then, because your sample scenario sends HTML-based messages, you create a MIME body part and append your HTML message payload to it.

- 4. Finally, you can use the Session instance to open up a connection and send the message. Here, the connection parameters specified in the Mail destination are used to connect to the target SMTP server used to transmit the message.

```
@Stateless
@LocalBean
public class EmailAgentBean
{

@Resource(name="mail/Session")
private Session mailSession;

public void sendMessage(String sender,
                        String receiver,
                        String subject,
                        String body)
    throws MessagingException
{
    Transport transport = null;

    try
{
    MimeMessage message = new MimeMessage(mailSession);

InternetAddress[] recipients = {
    InternetAddress.parse(receiver),
    InternetAddress.parse(sender)};
message.setFrom(new InternetAddress(sender));
message.setRecipients(RecipientType.TO, recipients);
message.setSubject(subject, "UTF-8");

Multipart multipart = new MimeMultipart("alternative");
MimeBodyPart htmlPart = new MimeBodyPart();
htmlPart.setContent(body, "text/html");
multipart.addBodyPart(htmlPart);
message.setContent(multipart);

transport = mailSession.getTransport();
transport.connect();
transport.sendMessage(message, message.getAllRecipients());
}
catch (Exception ex)
{
    logger.error(ex.getMessage());
    throw new MessagingException(ex.getMessage(), ex);
}
finally
{
    if (transport != null)
    {
        try
        {
            transport.close();
        }
        catch (MessagingException me) { }
    }
} // -- public void sendMessage() -- //
...
```

Listing 6.19 Sending an Email Message Using the javax.mail Library

You can test this functionality in the sample application by clicking on the EMAIL icon (the envelope) available in the Actions column of the INCIDENT WORKLIST screen, as shown in Figure 6.43. If you run into issues, then you can turn on debugging for your Mail destination by setting the mail.debug property to true. The debug output will be provided by the System.out logger. You may have to tweak the log level of the logger to enable the log output to show up at runtime.

![](img/cf7012644082c115a2181376d9b7486d_281_0.png)

Figure 6.43 Testing the Email Notification Function in the Sample Application

## 6.4 Using the Document Service

In Section 6.2, you learned how to use the Persistence Service to store structured data in relational databases. By structured data, we’re referring to data that is highly organized and predictable in nature. Such data fits nicely into two-dimensional tables and is easy to analyze using query languages, such as SQL.

Although many enterprise applications work pretty much exclusively with structured data, there are times when an application may also need to deal with raw, unstructured data, such as document attachments, social media feeds, and so on. Although you could technically store this raw data in the database along with everything else, to do so would be tantamount to stacking boxes in the archives closet; no one will ever see the data again. In order to be able to do productive things with this unstructured data, you need something more than just a simple data store. What you need is a content repository.

In addition to providing data storage capabilities, content repositories also provide several other important value-add features, including the following:

- Versioning
- Security using access control lists (ACLs)
- Indexing
- Advanced query and search capabilities

Collectively, these features allow you to get more out of your unstructured data.
