| **javax.swing.JComponent 1.2** |
| --- |
| • `void setTransferHandler(TransferHandler handler) 1.4`<br>sets a transfer handler to handle data transfer operations (cut, copy, paste, drag, drop). |

| **javax.swing.TransferHandler 1.4** |
| --- |
| • `TransferHandler(String propertyName)`<br>constructs a transfer handler that reads or writes the JavaBeans component property with the given name when a data transfer operation is executed. |

| **javax.swing.JFileChooser 1.2**<br>**javax.swing.JColorChooser 1.2**<br>**javax.swing.text.JTextComponent 1.2**<br>**javax.swing.JList 1.2**<br>**javax.swing.JTable 1.2**<br>**javax.swing.JTree 1.2** |
| --- |
| • `void setDragEnabled(boolean b) 1.4`<br>enables or disables dragging of data out of this component. |

# ### 11.14.2 Drag Sources

In the previous section, you saw how to take advantage of the basic drag-and-drop support in Swing. In this section, we’ll show you how to configure any component as a drag source. In the next section, we’ll discuss drop targets and present a sample component that is both a source and a target for images.

To customize the drag-and-drop behavior of a Swing component, subclass the `TransferHandler` class. First, override the `getSourceActions` method to indicate which actions (copy, move, link) your component supports. Next, override the `createTransferable` method that produces a `Transferable` object, following the same process that you use for copying to the clipboard.

In our sample program, we drag images out of a `JList` that is filled with image icons (see Figure 11.45). Here is the implementation of the `createTransferable` method. The selected image is simply placed into an `ImageTransferable` wrapper.