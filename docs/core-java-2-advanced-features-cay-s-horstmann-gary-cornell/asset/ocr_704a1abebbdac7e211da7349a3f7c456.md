```
```java
Clipboard clipboard = Toolkit.getDefaultToolkit().getSystemClipboard();
```
```

For strings to be transferred to the clipboard, they must be wrapped into `StringSelection` objects.

```
```java
String text = ...;
StringSelection selection = new StringSelection(text);
```
```

The actual transfer is done by a call to `setContents`, which takes a `StringSelection` object and a `ClipboardOwner` as parameters. If you are not interested in designating a clipboard owner, set the second parameter to `null`.

```
```java
clipboard.setContents(selection, null);
```
```

Here is the reverse operation—reading a string from the clipboard:

```
```java
DataFlavor flavor = DataFlavor.stringFlavor;
if (clipboard.isDataFlavorAvailable(flavor))
    String text = (String) clipboard.getData(flavor);
```
```

Listing 11.17 is a program that demonstrates cutting and pasting between a Java application and the system clipboard. If you select some text in the text area and click Copy, the selection is copied to the system clipboard. You can then paste it into any text editor (see Figure 11.40). Conversely, when you copy text from the text editor, you can paste it into our sample program.

![](bbox=[0.107, 0.548, 0.806, 0.831])

**Figure 11.40** The TextTransferTest program