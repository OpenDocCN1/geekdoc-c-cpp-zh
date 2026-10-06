# # Introduction to Qt Jambi

+   - Getting Started with Qt Jambi
- Using Qt Jambi in the Eclipse IDE
- Integrating C++ Components with Qt Jambi

Qt Jambi is the Java edition of the Qt application development framework. At the heart of Qt Jambi are the C++ libraries that form Qt, made available to Java programmers through the Java Native Interface (JNI). Although considerable effort has gone into making Qt Jambi integrate smoothly with Java and to make its API natural to Java programmers, C++/Qt programmers will still find the API familiar and predictable. All the classes are documented using Javadoc http://www.trolltech.com/qtjambi.

Now until, Java programmers had to make do with AWT, Swing, SWT, and similar GUI class libraries, none of which are as convenient or as powerful as Qt. For example, in the traditional GUI class libraries, connecting a user action, such as clicking a button, to a corresponding method involves writing an event listener class; in Qt Jambi, only one line of code is required to achieve the same thing. Qt's layout managers are much easier to use than Swing's BoxLayout GridLayout, and they produce better-looking results.

Qt Jambi applications can have main windows with menu bars, toolbars, dock windows, and a status bar, just like Qt applications written in C++. They also have the native look and feel of the platform they are running on, and they respect the user's preferences regarding themes, colors, fonts, and so on. With the full power of Qt under the hood, Qt Jambi applications can take advantage of Qt's powerful 2D graphics architecture (notably the graphics framework) and of extensions such as OpenGL.

The benefits of Qt Jambi are not limited to Java programmers. In particular, C++ programmers can make their custom Qt components available to Java programmers using the same generator tool that Trolltech uses to make the Qt API available in Qt Jambi.

In this appendix, we will show how Java programmers can start using Qt Jambi to create GUI applications. Then we will show how to make use of Qt Jambi in Eclipse, and finally we will show how to make custom C++ components available to Qt Jambi programmers. This appendix assumes that you are familiar with C++/Qt programming and with Java. Qt Jambi requires Java 1.5 or later.

# ## Getting Started with Qt Jambi

In this section, we will develop a small Java application that presents the window