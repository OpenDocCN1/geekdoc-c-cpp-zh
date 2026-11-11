Then send it off:

```
Transport tr = mailSession.getTransport();
tr.connect(null, password);
tr.sendMessage(message, message.getAllRecipients());
tr.close();
```

The program in Listing 4.9 reads the message from a text file of the format

+   - Sender
+   - Recipient
+   - Subject
+   - Message text (any number of lines)

To run the program, download the JavaMail implementation from https://javaee.github.io/javamail. You also need the JAR file for the Java Activation Framework—get it from http://www.oracle.com/technetwork/java/javase/jaf-135115.html or search on Maven Central. Then run

```
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

# Listing 4.9  `mail/MailTest.java`

```
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