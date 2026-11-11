| API element | Description |
|---|---|
| `javax.swing.text.JTextComponent.DropLocation` | 6 |
| `int getIndex()` | The index at which to insert the data. |

# 11.15 Platform Integration

We finish this chapter with several features for making Java applications feel more like native applications. The splash screen feature allows your application to display a splash screen as the virtual machine starts up. The java.awt.Desktop class lets you launch native applications such as the default browser and e-mail program. Finally, you now have access to the system tray and can clutter it up with icons, just like so many native applications do.

# 11.15.1 Splash Screens

A common complaint about Java applications is their long startup time. The Java virtual machine takes some time to load all required classes, particularly for a Swing application that needs to pull in large amounts of Swing and AWT library code. Users dislike applications that take a long time to bring up an initial screen, and they might even try launching the application multiple times if they suspect the first launch was unsuccessful. The remedy is a splash screen—a small window that appears quickly, telling the user that the application has been launched successfully.

Of course, you can put up a window as soon as your main method starts. However, the main method is only launched after the class loader has loaded all dependent classes, which might take a while.

Instead, you can ask the virtual machine to show an image immediately on launch. There are two mechanisms for specifying that image. You can use the -splash command-line option:

```
```java
java -splash:myimage.png MyApp
```
```

Alternatively, you can specify it in the manifest of a JAR file:

```
```text
Main-Class: MyApp
SplashScreen-Image: myimage.gif
```
```

The image is displayed immediately and automatically disappears when the first AWT window is made visible. You can supply any GIF, JPEG, or PNG image. Animation (in GIF) and transparency (GIF and PNG) are supported.