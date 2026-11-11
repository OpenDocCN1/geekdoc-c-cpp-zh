# Listing 11.22  *(Continued)*

```
```java
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
      setLayoutOrientation(List.HORIZONTAL_WRAP);
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
}
```
```