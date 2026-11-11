
- **java.awt.datatransfer.DataFlavor 1.1 (Continued)**
  - `boolean isMimeTypeEqual(String mimeType)` tests whether this data flavor has the given MIME type.
  - `String getHumanPresentableName()` returns the human-presentable name for the data format of this data flavor.
  - `Class getRepresentationClass()` returns a Class object that represents the class of the object that a Transferable object will return when called with this data flavor. This is either the class parameter of the MIME type or InputStream.

- **java.awt.datatransfer.Clipboard 1.1**
  - `DataFlavor[] getAvailableDataFlavors()` 5.0 returns an array of the available flavors.
  - `void addFlavorListener(FlavorListener listener)` 5.0 adds a listener that is notified when the set of available flavors changes.

- **java.awt.datatransfer.Transferable 1.1**
  - `DataFlavor[] getTransferDataFlavors()` returns an array of the supported flavors.

- **java.awt.datatransfer.FlavorListener 5.0**
  - `void flavorsChanged(FlavorEvent event)` is called when a clipboard's set of available flavors changes.

## 11.13.4 Building an Image Transferable

Objects that you want to transfer via the clipboard must implement the `Transferable` interface. The `StringSelection` class is currently the only public class in the Java standard library that implements the `Transferable` interface. In this section, you will see how to transfer images into the clipboard. Since Java does not supply a class for image transfer, you must implement it yourself.

The class is completely trivial. It simply reports that the only available data format is `DataFlavor.imageFlavor`, and it holds an image object.

```java
class ImageTransferable implements Transferable
{
    private Image theImage;

    public ImageTransferable(Image image)
    {
        theImage = image;
    }

    public DataFlavor[] getTransferDataFlavors()
    {
        return new DataFlavor[] { DataFlavor.imageFlavor };
    }

    public boolean isDataFlavorSupported(DataFlavor flavor)
    {
        return flavor.equals(DataFlavor.imageFlavor);
    }

    public Object getTransferData(DataFlavor flavor)
        throws UnsupportedFlavorException
    {
        if(flavor.equals(DataFlavor.imageFlavor))
        {
            return theImage;
        }
        else
        {
            throw new UnsupportedFlavorException(flavor);
        }
    }
}
```

> NOTE: Java SE supplies the `DataFlavor.imageFlavor` constant and does all the heavy lifting to convert between Java images and native clipboard images. Curiously, however, it does not supply the wrapper class that is necessary to place images onto the clipboard.

The program in Listing 11.18 demonstrates the transfer of images between a Java application and the system clipboard. When the program starts, it generates an image containing a red circle. Click the Copy button to copy the image to the clipboard and then paste it into another application (see Figure 11.41). From another application, copy an image into the system clipboard. Then click the Paste button and see the image being pasted into the example program (see Figure 11.42).

![](img/7dd923a566750151a3aab0dacd0cdaa5_916_0.png)

**Figure 11.41** Copying from a Java program to a native program

![](img/7dd923a566750151a3aab0dacd0cdaa5_916_1.png)

**Figure 11.42** Copying from a native program to a Java program

The program is a straightforward modification of the text transfer program. The data flavor is now `DataFlavor.imageFlavor`, and we use the `ImageTransferable` class to transfer an image to the system clipboard.

### Listing 11.18 `imageTransfer/ImageTransferFrame.java`

```java
package imageTransfer;

import java.awt.*;
import java.awt.datatransfer.*;
import java.awt.image.*;
import java.io.*;

import javax.swing.*;

/**
 * This frame has an image label and buttons for copying and pasting an image.
 */
class ImageTransferFrame extends JFrame
{
    private JLabel label;
    private Image image;
    private static final int IMAGE_WIDTH = 300;
    private static final int IMAGE_HEIGHT = 300;

    public ImageTransferFrame()
    {
        label = new JLabel();
        image = new BufferedImage(IMAGE_WIDTH, IMAGE_HEIGHT, BufferedImage.TYPE_INT_ARGB);
        Graphics g = image.getGraphics();
        g.setColor(Color.WHITE);
        g.fillRect(0, 0, IMAGE_WIDTH, IMAGE_HEIGHT);
        g.setColor(Color.RED);
        g.fillOval(IMAGE_WIDTH / 4, IMAGE_WIDTH / 4, IMAGE_WIDTH / 2, IMAGE_HEIGHT / 2);

        label.setIcon(new ImageIcon(image));
        add(new JScrollPane(label), BorderLayout.CENTER);
        JPanel panel = new JPanel();

        JButton copyButton = new JButton("Copy");
        panel.add(copyButton);
        copyButton.addActionListener(event -> copy());

        JButton pasteButton = new JButton("Paste");
        panel.add(pasteButton);
        pasteButton.addActionListener(event -> paste());

        add(panel, BorderLayout.SOUTH);
        pack();
    }

    /**
     * Copies the current image to the system clipboard.
     */
    private void copy()
    {
        Clipboard clipboard = Toolkit.getDefaultToolkit().getSystemClipboard();
        ImageTransferable selection = new ImageTransferable(image);
        clipboard.setContents(selection, null);
    }

    /**
     * Pastes the image from the system clipboard into the image label.
     */
    private void paste()
    {
        Clipboard clipboard = Toolkit.getDefaultToolkit().getSystemClipboard();
        DataFlavor flavor = DataFlavor.imageFlavor;
        if (clipboard.isDataFlavorAvailable(flavor))
        {
            try
            {
                Image image = (Image) clipboard.getData(flavor);
                label.setIcon(new ImageIcon(image));
            }
            catch (UnsupportedFlavorException | IOException ex)
            {
                JOptionPane.showMessageDialog(this, ex);
            }
        }
    }
}
```

## 11.13.5 Transferring Java Objects via the System Clipboard

Suppose you want to copy and paste objects from one Java application to another. You can accomplish this task by placing serialized Java objects onto the system clipboard.

The program in Listing 11.19 demonstrates this capability. The program shows a color chooser. The Copy button copies the current color to the system clipboard as a serialized Color object. The Paste button checks whether the system clipboard contains a serialized Color object. If so, it fetches the color and sets it as the current choice of the color chooser.

You can transfer the serialized object between two Java applications (see Figure 11.43). Run two copies of the SerialTransferTest program. Click Copy in the

### Listing 11.19 `serialTransfer/SerialTransferFrame.java`

```java
package serialTransfer;

import java.awt.*;
import java.awt.datatransfer.*;
import java.awt.event.*;
import java.io.*;
import javax.swing.*;

/**
 * This frame contains a color chooser, and copy and paste buttons.
 */
class SerialTransferFrame extends JFrame
{
   private JColorChooser chooser;

   public SerialTransferFrame()
   {
      chooser = new JColorChooser();
      add(chooser, BorderLayout.CENTER);
      JPanel panel = new JPanel();

      JButton copyButton = new JButton("Copy");
      panel.add(copyButton);
      copyButton.addActionListener(event -> copy());

      JButton pasteButton = new JButton("Paste");
      panel.add(pasteButton);
      pasteButton.addActionListener(event -> paste());

      add(panel, BorderLayout.SOUTH);
      pack();
   }

   /**
    * Copies the chooser's color into the system clipboard.
    */
   private void copy()
   {
      Clipboard clipboard = Toolkit.getDefaultToolkit().getSystemClipboard();
      Color color = chooser.getColor();
      SerialTransferable selection = new SerialTransferable(color);
      clipboard.setContents(selection, null);
   }

   /**
    * Pastes the color from the system clipboard into the chooser.
    */
```
