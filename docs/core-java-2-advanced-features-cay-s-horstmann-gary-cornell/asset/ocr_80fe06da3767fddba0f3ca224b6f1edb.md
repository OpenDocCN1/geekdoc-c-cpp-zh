```
```java
private void paste()
{
    Clipboard clipboard = Toolkit.getDefaultToolkit().getSystemClipboard();
    try
    {
        DataFlavor flavor = new DataFlavor(
            "application/x-java-serialized-object;class=java.awt.Color");
        if (clipboard.isDataFlavorAvailable(flavor))
        {
            Color color = (Color) clipboard.getData(flavor);
            chooser.setColor(color);
        }
    }
    catch (ClassNotFoundException | UnsupportedFlavorException | IOException ex)
    {
        JOptionPane.showMessageDialog(this, ex);
    }
}
}

/**
 * This class is a wrapper for the data transfer of serialized objects.
 */
class SerialTransferrable implements Transferable
{
    private Serializable obj;

    /**
     * Constructs the selection.
     * @param o any serializable object
     */
    SerialTransferrable(Serializable o)
    {
        obj = o;
    }

    public DataFlavor[] getTransferDataFlavors()
    {
        DataFlavor[] flavors = new DataFlavor[2];
        Class<?> type = obj.getClass();
        String mimeType = "application/x-java-serialized-object;class=" + type.getName();
        try
        {
            flavors[0] = new DataFlavor(mimeType);
            flavors[1] = DataFlavor.stringFlavor;
            return flavors;
        }
```
```

(Continues)