
Serialization is too fragile for long-term storage. Of course, if you disagree, you can save serialized objects in byte arrays.

For additional flexibility, there are multiple parallel trees. Each program user has one tree; an additional tree, called the system tree, is available for settings that are common to all users. The Preferences class uses the operating system’s notion of the “current user” for accessing the appropriate user tree.

To access a node in the tree, start with the user or system root:

```java
Preferences root = Preferences.userRoot();
```

or

```java
Preferences root = Preferences.systemRoot();
```

Then access the node. You can simply provide a node path name:

```java
Preferences node = root.node("/com/mycompany/myapp");
```

A convenient shortcut gets a node whose path name equals the package name of a class. Simply take an object of that class and call

```java
Preferences node = Preferences.userNodeForPackage(obj.getClass());
```

or

```java
Preferences node = Preferences.systemNodeForPackage(obj.getClass());
```

Typically, obj will be the `this` reference.

Once you have a node, you can access the key/value table with methods

```java
String get(String key, String defval)
int getInt(String key, int defval)
long getLong(String key, long defval)
float getFloat(String key, float defval)
double getDouble(String key, double defval)
boolean getBoolean(String key, boolean defval)
byte[] getByteArray(String key, byte[] defval)
```

Note that you must specify a default value when reading the information, in case the repository data is not available. Defaults are required for several reasons. The data might be missing because the user never specified a preference. Certain resource-constrained platforms might not have a repository, and mobile devices might be temporarily disconnected from the repository.

Conversely, you can write data to the repository with put methods such as

```java
put(String key, String value)
putInt(String key, int value)
```

and so on.

You can enumerate all keys stored in a node with the method

```java
String[] keys()
```

There is currently no way to find out the type of the value of a particular key.

> **NOTE:** Node names and keys are limited to 80 characters, and string values to 8192 characters.

Central repositories such as the Windows registry traditionally suffer from two problems:

- They turn into a “dumping ground” filled with obsolete information.
- Configuration data gets entangled into the repository, making it difficult to move preferences to a new platform.

The Preferences class has a solution for the second problem. You can export the preferences of a subtree (or, less commonly, a single node) by calling the methods

```java
void exportSubtree(OutputStream out)
void exportNode(OutputStream out)
```

The data are saved in XML format. You can import them into another repository by calling

```java
void importPreferences(InputStream in)
```

Here is a sample file:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE preferences SYSTEM "http://java.sun.com/dtd/preferences.dtd">
<preferences EXTERNAL_XML_VERSION="1.0">
    <root type="user">
        <map/>
        <node name="com">
            <map/>
            <node name="horstmann">
                <map/>
                <node name="corejava">
                    <map>
                        <entry key="height" value="200.0"/>
                        <entry key="left" value="1027.0"/>
                        <entry key="filename" value="/home/cay/books/cj11/code/v11ch11/raven.html"/>
                        <entry key="top" value="380.0"/>
                        <entry key="width" value="300.0"/>
                    </map>
                </node>
            </node>
        </node>
    </root>
</preferences>
```

If your program uses preferences, you should give your users the opportunity of exporting and importing them, so they can easily migrate their settings from one computer to another. The program in Listing 10.7 demonstrates this technique. The program simply saves the window location and the last loaded filename. Try resizing the window, then export your preferences, move the window, exit, and restart the application. The window will be just like you left it when you exited. Import your preferences, and the window reverts to its prior location.

### Listing 10.7 `preferences/ImageViewer.java`

```java
package preferences;

import java.awt.EventQueue;
import java.awt.event.*;
import java.io.*;
import java.util.prefs.*;
import javax.swing.*;

/**
 * A program to test preference settings. The program remembers the
 * frame position, size, and last selected file.
 * @version 1.10 2018-04-10
 * @author Cay Horstmann
 */
public class ImageViewer
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() -> {
         var frame = new ImageViewerFrame();
         frame.setTitle("ImageViewer");
         frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
         frame.setVisible(true);
      });
   }
}

/**
 * An image viewer that restores position, size, and image from user
 * preferences and updates the preferences upon exit.
 */
class ImageViewerFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 300;
   private static final int DEFAULT_HEIGHT = 200;
   private String image;

   public ImageViewerFrame()
   {
      Preferences root = Preferences.userRoot();
      Preferences node = root.node("/com/horstmann/corejava/ImageViewer");
      // get position, size, title from properties
      int left = node.getInt("left", 0);
      int top = node.getInt("top", 0);
      int width = node.getInt("width", DEFAULT_WIDTH);
      int height = node.getInt("height", DEFAULT_HEIGHT);
      setBounds(left, top, width, height);
      image = node.get("image", null);
      var label = new JLabel();
      if (image != null) label.setIcon(new ImageIcon(image));

      addWindowListener(new WindowAdapter()
      {
         public void windowClosing(WindowEvent event)
         {
            node.putInt("left", getX());
            node.putInt("top", getY());
            node.putInt("width", getWidth());
            node.putInt("height", getHeight());
            if (image != null) node.put("image", image);
         }
      });

      // use a label to display the images
      add(label);

      // set up the file chooser
      var chooser = new JFileChooser();
      chooser.setCurrentDirectory(new File("."));

      // set up the menu bar
      var menuBar = new JMenuBar();
      setJMenuBar(menuBar);

      var menu = new JMenu("File");
      menuBar.add(menu);

      var openItem = new JMenuItem("Open");
      menu.add(openItem);
      openItem.addActionListener(event -> {

         // show file chooser dialog
         int result = chooser.showOpenDialog(null);

         // if file selected, set it as icon of the label
         if (result == JFileChooser.APPROVE_OPTION)
         {
            image = chooser.getSelectedFile().getPath();
            label.setIcon(new ImageIcon(image));
         }
      });

      var exitItem = new JMenuItem("Exit");
      menu.add(exitItem);
      exitItem.addActionListener(event -> System.exit(0));
   }
}
```

| java.util.prefs.Preferences 1.4 |
| --- |
| • `Preferences userRoot()`<br>returns the root preferences node of the user of the calling program.<br>• `Preferences systemRoot()`<br>returns the systemwide root preferences node.<br>• `Preferences node(String path)`<br>returns a node that can be reached from the current node by the given path. If path is absolute (that is, starts with a /), then the node is located starting from the root of the tree containing this preference node. If there isn't a node with the given path, it is created.<br>• `Preferences userNodeForPackage(Class cl)`<br>• `Preferences systemNodeForPackage(Class cl)`<br>returns a node in the current user's tree or the system tree whose absolute node path corresponds to the package name of the class cl.<br>• `String[] keys()`<br>returns all keys belonging to this node. |
