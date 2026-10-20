# Error-Prevention Tip 27.1

The applet in Fig. 27.2 must be run from a web browser to show the results of displaying another web page. The appletviewer is capable only of executing applets—it ignores all other HTML tags. If the websites in the program contained Java applets, only those applets would appear in the appletviewer when the user selected a website. [Note: Each applet would execute in a separate appletviewer window.]

# 27.3 Reading a File on a Web Server

The application in Fig. 27.3 uses Swing GUI component JEditorPane (from package javax.swing) to display the contents of a file on a web server. The user enters a URL in the JTextField at the top of the window, and the application displays the corresponding document (if it exists) in the JEditorPane. Class JEditorPane is able to render plain text and basic HTML-formatted text, as illustrated in the two screen captures (Fig. 27.4), so this application acts as a simple web browser. The application also demonstrates how to process HyperlinkEvents when the user clicks a hyperlink in the HTML document. The techniques shown in this example can also be used in applets. However, an applet is allowed to read files only on the server from which it was downloaded. [Note: This program might not work if your web browser must access the web through a proxy server. If you create a JNLP document for this program and use Java Web Start to launch it, Java Web Start will use the proxy server settings from your default web browser. See Chapters 23–24 for more information on Java Web Start.]

```
```java
// Fig. 27.3: ReadServerFile.java
// Reading a file by opening a connection through a URL.
import java.awt.BorderLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.IOException;
import javax.swing.JEditorPane;
import javax.swing.JFrame;
import javax.swing.JOptionPane;
import javax.swing.JScrollPane;
import javax.swing.JTextField;
import javax.swing.event.HyperlinkEvent;
import javax.swing.event.HyperlinkListener;
public class ReadServerFile extends JFrame
{
    private JTextField enterField; // JTextField to enter site name
    private JEditorPane contentsArea; // to display website
    // set up GUI
    public ReadServerFile()
    {
        ...
    }
}
```
```

Fig. 27.3 | Reading a file by opening a connection through a URL. (Part I of 2.)