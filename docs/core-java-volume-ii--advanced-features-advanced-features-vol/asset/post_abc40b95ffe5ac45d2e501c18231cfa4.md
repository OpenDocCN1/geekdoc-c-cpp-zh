
### Listing 4.8 (Continued)

```java
106    String urlString = "" + props.remove("url");
107    String contentType = "" + props.remove("Content-Type");
108    if (contentType.equals("multipart/form-data")) {
110        var generator = new Random();
111        String boundary = new BigInteger(256, generator).toString();
112        contentType += ";boundary=" + boundary;
113        props.replaceAll((k, v) ->
114            v.toString().startsWith("file:")
115                ? propsPath.getParent().resolve(Paths.get(v.toString().substring(7)))
116                : v);
117    }
118    String result = doPost(urlString, contentType, props);
119    System.out.println(result);
120    }
121
122    public static String doPost(String url, String contentType, Map<Object, Object> data)
123        throws IOException, URISyntaxException, InterruptedException
124    {
125        HttpClient client = HttpClient.newBuilder()
126            .followRedirects(HttpClient.Redirect.ALWAYS).build();
127
128        BodyPublisher publisher = null;
129        if (contentType.startsWith("multipart/form-data")) {
131            String boundary = contentType.substring(contentType.lastIndexOf('=') + 1);
132            publisher = MoreBodyPublishers.ofMimeMultipartData(data, boundary);
133        }
134        else if (contentType.equals("application/x-www-form-urlencoded")) {
135            publisher = MoreBodyPublishers.ofFormData(data);
136        } else
137        {
138            contentType = "application/json";
139            publisher = MoreBodyPublishers.ofSimpleJSON(data);
140        }
141
142        HttpRequest request = HttpRequest.newBuilder()
143            .uri(new URI(url))
144            .header("Content-Type", contentType)
145            .POST(publisher)
146            .build();
147        HttpResponse<String> response
148            = client.send(request, HttpResponse.BodyHandlers.ofString());
149        return response.body();
150    }
151 }
```

### java.net.HttpClient 11

- `static HttpClient newHttpClient()`  
  yields an HttpClient with a default configuration.
- `static HttpClient.Builder newBuilder()`  
  yields a builder for building an HttpClient.
- `<T> HttpResponse<T> send(HttpRequest request, HttpResponse.BodyHandler<T> responseBodyHandler)`
- `<T> CompletableFuture<HttpResponse<T>> sendAsync(HttpRequest request, HttpResponse.BodyHandler<T> responseBodyHandler)`  
  makes a synchronous or asynchronous request and processes the response body with the given handler.

### java.net.HttpClient.Builder 11

- `HttpClient build()`  
  yields an HttpClient with the properties configured by this builder.
- `HttpClient.Builder followRedirects(HttpClient.Redirect policy)`  
  sets the redirect policy to one of the values ALWAYS, NEVER, or NORMAL (only refuse redirects from HTTPS to HTTP) of the HttpClient.Redirect enumeration.
- `HttpClient.Builder executor(Executor executor)`  
  sets the executor for asynchronous requests.

### java.net.HttpRequest 11

- `static HttpRequest.Builder newBuilder()`  
  yields a builder for building an HttpRequest.

### java.net.HttpRequest.Builder 11

- `HttpRequest build()`  
  yields an HttpRequest with the properties configured by this builder.
- `HttpRequest.Builder uri(URI uri)`  
  sets the URI for this request.
- `HttpRequest.Builder header(String name, String value)`  
  sets a request header for this request.

### java.net.HttpRequest.Builder 11 (Continued)

| 方法 | 说明 |
| --- | --- |
| `HttpRequest.Builder GET()`<br>`HttpRequest.Builder DELETE()`<br>`HttpRequest.Builder POST(HttpRequest.BodyPublisher bodyPublisher)`<br>`HttpRequest.Builder PUT(HttpRequest.BodyPublisher bodyPublisher)` | sets the request method and body for this request. |

### java.net.HttpResponse<T> 11

| 方法 | 说明 |
| --- | --- |
| `T body()` | yields the body of this response. |
| `int statusCode()` | yields the status code for this response. |
| `HttpHeaders headers()` | yields the response headers. |

### java.net.HttpHeaders 11

| 方法 | 说明 |
| --- | --- |
| `Map<String,List<String>> map()` | yields a Map of these headers. |
| `Optional<String> firstValue(String name)` | the first value with the given name in these headers, if present. |

## 4.5 Sending E-Mail

In the past, it was simple to write a program that sends e-mail by making a socket connection to port 25, the SMTP port, of a mail server. The Simple Mail Transport Protocol (SMTP) describes the format for e-mail messages. Once you are connected to the server, send a mail header (in the SMTP format, which is easy to generate), followed by the mail message.

Here are the details:

1. Open a socket to your host.

   ```java
   var s = new Socket("mail.yourserver.com", 25); // 25 is SMTP
   var out = new PrintWriter(s.getOutputStream(), StandardCharsets.UTF_8);
   ```

2. Send the following information to the print stream:

   ```text
   HELO sending host
   MAIL FROM: sender e-mail address
   RCPT TO: recipient e-mail address
   DATA
   Subject: subject
   (blank line)
   mail message (any number of lines)
   .
   QUIT
   ```

The SMTP specification (RFC 821) states that lines must be terminated with `\r` followed by `\n`.

It used to be that SMTP servers were often willing to route e-mail from anyone. However, in these days of spam floods, most servers have built-in checks and only accept requests from users or IP address ranges that they trust. Authentication usually happens over secure socket connections.

Implementing these authentication schemes manually would be very tedious. Instead, we will show you how to use the JavaMail API to send e-mail from a Java program.

Download JavaMail from www.oracle.com/technetwork/java/javamail and unzip it somewhere on your hard disk.

To use JavaMail, you need to set up some properties that depend on your mail server. For example, with GMail, you use

```properties
mail.transport.protocol=smtps
mail.smtps.auth=true
mail.smtps.host=smtp.gmail.com
mail.smtps.user=accountname@gmail.com
```

Our sample program reads these from a property file.

For security reasons, we don’t put the password into the property file but instead prompt for it.

Read in the property file, then get a mail session like this:

```java
Session mailSession = Session.getDefaultInstance(props);
```

Make a message with the desired sender, recipient, subject, and message text:

```java
var message = new MimeMessage(mailSession);
message.setFrom(new InternetAddress(from));
message.addRecipient(RecipientType.TO, new InternetAddress(to));
message.setSubject(subject);
message.setText(builder.toString());
```

Then send it off:

```java
Transport tr = mailSession.getTransport();
tr.connect(null, password);
tr.sendMessage(message, message.getAllRecipients());
tr.close();
```

The program in Listing 4.9 reads the message from a text file of the format

- Sender
- Recipient
- Subject
- Message text (any number of lines)

To run the program, download the JavaMail implementation from https://javaee.github.io/javamail. You also need the JAR file for the Java Activation Framework—get it from http://www.oracle.com/technetwork/java/javase/jaf-135115.html or search on Maven Central. Then run

```bash
java -classpath .:javax.mail.jar:activation-1.1.1.jar path/to/message.txt
```

At the time of this writing, GMail does not check the veracity of the information—you can supply any sender you like. (Keep this in mind the next time you get an e-mail message from president@whitehouse.gov inviting you to a black-tie affair on the front lawn.)

> **TIP:** If you can’t figure out why your mail connection isn’t working, call
>
> ```java
> mailSession.setDebug(true);
> ```
>
> and check out the messages. Also, the JavaMail API FAQ has some useful debugging hints.

### Listing 4.9 `mail/MailTest.java`

```java
1  package mail;

3  import java.io.*;
4  import java.nio.charset.*;
5  import java.nio.file.*;
6  import java.util.*;
7  import javax.mail.*;
8  import javax.mail.internet.*;
9  import javax.mail.internet.MimeMessage.RecipientType;

11 /**
12  * This program shows how to use JavaMail to send mail messages.
13  * @author Cay Horstmann
14  * @version 1.01 2018-03-17
```
