
### javax.swing.TransferHandler 1.4

- `int getSourceActions(JComponent c)`  
  override to return the allowable source actions (bitwise OR combination of COPY, MOVE, and LINK) when dragging from the given component.
- `protected Transferable createTransferable(JComponent source)`  
  override to create the `Transferable` for the data that is to be dragged.
- `void exportAsDrag(JComponent comp, InputEvent e, int action)`  
  starts a drag gesture from the given component. The action is COPY, MOVE, or LINK.
- `protected void exportDone(JComponent source, Transferable data, int action)`  
  override to adjust the drag source after a successful transfer.

## 11.14.3 Drop Targets

In this section, we’ll show you how to implement a drop target. Our example is again a `JList` with image icons. We’ll add drop support so that users can drop images into the list.

To make a component into a drop target, set a `TransferHandler` and implement the `canImport` and `importData` methods.

> **NOTE:** You can add a transfer handler to a `JFrame`. This is most commonly used for dropping files into an application. Valid drop locations include the frame decorations and the menu bar, but not components contained in the frame (which have their own transfer handlers).

The `canImport` method is called continuously as the user moves the mouse over the drop target component. Return true if a drop is allowed. This information affects the cursor icon that gives visual feedback whether the drop is allowed.

The `canImport` method has a parameter of type `TransferHandler.TransferSupport`. Through this parameter, you can obtain the drop action chosen by the user, the drop location, and the data to be transferred. (Before Java SE 6, a different `canImport` method was called that only supplies a list of data flavors.)

In the `canImport` method, you can also override the user drop action. For example, if a user chose the move action but it would be inappropriate to remove the original, you can force the transfer handler to use a copy action instead.

Here is a typical example. The image list component is willing to accept drops of file lists and images. However, if a file list is dragged into the component, a

### Table 11.8 Drop Modes

| Component | Supported Drop Modes |
|---|---|
| JList, JTree | ON, INSERT, ON_OR_INSERT, USE_SELECTION |
| JTable | ON, INSERT, ON_OR_INSERT, INSERT_ROWS, INSERT_COLS, ON_OR_INSERT_ROWS, ON_OR_INSERT_COLS, USE_SELECTION |
| JTextComponent | INSERT, USE_SELECTION (actually moves the caret, not the selection) |

One data type that is commonly used for drag and drop is the `DataFlavor.javaFileListFlavor`. A file list describes a set of files that are dropped onto the target. The transfer data is an object of type `List<File>`. Here is the code for retrieving the files:

```java
DataFlavor[] flavors = transferable.getTransferDataFlavors();
if (Arrays.asList(flavors).contains(DataFlavor.javaFileListFlavor))
{
    List<File> fileList = (List<File>) transferable.getTransferData(DataFlavor.javaFileListFlavor);
    for (File f : fileList)
    {
        do something with f;
    }
}
```

When dropping into one of the components listed in Table 11.8, you need to know precisely where to drop the data. Invoke the `getDropLocation` method on the `TransferSupport` parameter to find where the drop occurred. This method returns an object of a subclass of `TransferHandler.DropLocation`. The `JList`, `JTable`, `JTree`, and `JTextComponent` classes define subclasses that specify location in the particular data model. For example, a location in a list is simply an integer index, but a location in a tree is a tree path. Here is how we obtain the drop location in our image list:

```java
int index;
if (support.isDrop())
{
    JList.DropLocation location = (JList.DropLocation) support.getDropLocation();
    index = location.getIndex();
}
else index = model.size();
```

The `JList.DropLocation` subclass has a method `getIndex` that returns the index of the drop. (The `JTree.DropLocation` subclass has a method `getPath` instead.)

The `importData` method is also called when data are pasted into the component with the Ctrl+V keystroke. In that case, the `getDropLocation` method would throw an `IllegalStateException`. Therefore, if the `isDrop` method returns false, we simply append the pasted data to the end of the list.

When inserting into a list, table, or tree, you also need to check whether the data should be inserted between items or replace the item at the drop location. For a list, invoke the `isInsert` method of the `JList.DropLocation`. For the other components, see the API notes for their drop location classes at the end of this section.

To summarize, to turn a component into a drop target, add a transfer handler that specifies the following:

- When a dragged item can be accepted
- How the dropped data are imported

In addition, if you add drop support to a `JList`, `JTable`, `JTree`, or `JTextComponent`, you should set the drop mode.

Listing 11.22 shows the frame class of the program. Note that the `ImageList` class is both a drag source and a drop target. Try dragging images between the two lists. You can also drag image files from a file chooser of another program into the lists.

### Listing 11.22 dndImage/ImageListDemoFrame.java

```java
package dndImage;

import java.awt.*;
import java.awt.datatransfer.*;
import java.io.*;
import java.nio.file.*;
import java.util.*;
import java.util.List;
import javax.imageio.*;
import javax.swing.*;

public class ImageListDemoFrame extends JFrame
{
    private static final int DEFAULT_WIDTH = 600;
    private static final int DEFAULT_HEIGHT = 500;

    private ImageList list1;
    private ImageList list2;

    public ImageListDemoFrame()
    {
        setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

        list1 = new ImageList(Paths.get(getClass().getPackage().getName(), "images1"));
        list2 = new ImageList(Paths.get(getClass().getPackage().getName(), "images2"));

        setLayout(new GridLayout(2, 1));
        add(new JScrollPane(list1));
        add(new JScrollPane(list2));
    }
}

class ImageList extends JList<ImageIcon>
{
   public ImageList(Path dir)
   {
      DefaultListModel<ImageIcon> model = new DefaultListModel<>();
      try (DirectoryStream<Path> entries = Files.newDirectoryStream(dir))
      {
         for (Path entry : entries)
            model.addElement(new ImageIcon(entry.toString()));
      }
      catch (IOException ex)
      {
         ex.printStackTrace();
      }

      setModel(model);
      setVisibleRowCount(0);
      setLayoutOrientation(JList.HORIZONTAL_WRAP);
      setDragEnabled(true);
      setDropMode(DropMode.ON_OR_INSERT);
      setTransferHandler(new ImageListTransferHandler());
   }
}

class ImageListTransferHandler extends TransferHandler
{

   // support for drag

   public int getSourceActions(JComponent source)
   {
      return COPY_OR_MOVE;
   }

   protected Transferable createTransferable(JComponent source)
   {
      ImageList list = (ImageList) source;
      int index = list.getSelectedIndex();
      if (index < 0) return null;
      ImageIcon icon = list.getModel().getElementAt(index);
      return new ImageTransferable(icon.getImage());
   }

   protected void exportDone(JComponent source, Transferable data, int action)
   {
      if (action == MOVE)
      {
         ImageList list = (ImageList) source;
         int index = list.getSelectedIndex();
         if (index < 0) return;
         DefaultListModel<?> model = (DefaultListModel<?>) list.getModel();
         model.remove(index);
      }
   }

   // support for drop

   public boolean canImport(TransferSupport support)
   {
      if (support.isDataFlavorSupported(DataFlavor.javaFileListFlavor))
      {
         if (support.getUserDropAction() == MOVE) support.setDropAction(COPY);
         return true;
      }
      else return support.isDataFlavorSupported(DataFlavor.imageFlavor);
   }

   public boolean importData(TransferSupport support)
   {
      ImageList list = (ImageList) support.getComponent();
      DefaultListModel<ImageIcon> model = (DefaultListModel<ImageIcon>) list.getModel();

      Transferable transferable = support.getTransferable();
      List<DataFlavor> flavors = Arrays.asList(transferable.getTransferDataFlavors());

      List<Image> images = new ArrayList<>();

      try
      {
         if (flavors.contains(DataFlavor.javaFileListFlavor))
         {
            @SuppressWarnings("unchecked") List<File> fileList
                = (List<File>) transferable.getTransferData(DataFlavor.javaFileListFlavor);
            for (File f : fileList)
            {
               try
               {
                  images.add(ImageIO.read(f));
               }
               catch (IOException ex)
               {
```
