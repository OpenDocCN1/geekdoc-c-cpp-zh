or application from a web server so users can access it online, you’ll need to configure your web server correctly, as described at `java.sun.com/javase/6/docs/technotes/guides/javaws/developersguide/setup.html`.

# JNLP Document: information Element

The **information** element (lines 6–13) provides details about the program. The **title** element specifies a title for the program. The **vendor** element specifies who created the program. The values of these elements appear in Java Web Start’s security warnings and errors that are presented to the user. The title’s value also appears in the title bar of the window in which the program executes.

The **desktop** element that’s nested in the **shortcut** element (lines 9–11) tells Java Web Start to ask whether the user wishes to install a desktop shortcut. If the user accepts, an icon will appear on the desktop. The user can then launch the program in its own window by double-clicking the desktop icon. Note the syntax of the `<desktop/>` element—a so-called empty XML element. When nothing appears between an element’s start and end tags, the element can be written using one tag that ends with `/>`.

The **offline-allowed** element (line 12) indicates that once the program is installed on the user’s computer, it can be launched via Java Web Start—even when the computer is not connected to the Internet. This is particularly useful for any program that can be used with files stored on the user’s computer.

# JNLP Document: resources Element

The **resources** element (lines 15–18) contains two nested elements. The **java** element lists the minimum version of Java required to execute the program (line 16) and the **jar** element (line 17) specifies the location of the JAR file that contains the program and whether that JAR file contains the class that launches the program. There can be multiple jar elements, as you’ll see in the next chapter.

# JNLP Document: applet-desc Element

The **applet-desc** element (lines 20–25) is similar to the applet element in HTML. The name attribute specifies the applet’s name. The main-class attribute specifies the main applet class (the one that extends JApplet). The width and height attributes specify the width and height in pixels, respectively, of the window in which the applet will execute. Chapter 24 discusses a similar element for applications—`application-desc`.

# Launching the Applet with Java Web Start

You’re now ready to launch the applet via Java Web Start. There are several ways to do this. You can use the **javaws** command in a command window from the folder that contains the JNLP document, as in

```
javaws DrawTest.jnlp
```

You can also use your operating system’s file manager to locate the JNLP on your computer and double click its file name. Normally, the JNLP file is referenced from a web page via a hyperlink. The DrawTestWebPage.html document in Fig. 23.13 (which was saved in the same directory as the JNLP file) contains an anchor (a) element (line 4), which links to the DrawTest.jnlp file. Clicking this hyperlink in the web page downloads the JNLP file (in this case, it’s loaded from the local file system) and executes the corresponding applet.