```
```java
int result = chooser.showOpenDialog(parent);
```
```

or

```
```java
int result = chooser.showSaveDialog(parent);
```
```

The only difference between these calls is the label of the “approve button”—the button that the user clicks to finish the file selection. You can also call the showDialog method and pass an explicit text for the approve button:

```
```java
int result = chooser.showDialog(parent, "Select");
```
```

These calls return only when the user has approved, canceled, or dismissed the file dialog. The return value is JFileChooser.APPROVE_OPTION, JFileChooser.CANCEL_OPTION, or JFileChooser.ERROR_OPTION.

+   8. Get the selected file or files with the getSelectedFile() or getSelectedFiles() method. These methods return either a single File object or an array of File objects. If you just need the name of the file object, call its getPath method. For example:

```
```java
String filename = chooser.getSelectedFile().getPath();
```
```

For the most part, these steps are simple. The major difficulty with using a file dialog is to specify a subset of files from which the user should choose. For example, suppose the user should choose a GIF image file. Then, the file chooser should only display files with the extension .gif. It should also give the user some kind of feedback that the displayed files are of a particular category, such as “GIF Images.” But the situation can be more complex. If the user should choose a JPEG image file, the extension can be either .jpg or .jpeg. Instead of a way to codify these complexities, the designers of the file chooser provided a more elegant mechanism: to restrict the displayed files, supply an object that extends the abstract class javax.swing.filechooser.FileFilter. The file chooser passes each file to the file filter and displays only those files that the filter accepts.

At the time of this writing, two such subclasses are supplied: the default filter that accepts all files, and a filter that accepts all files with a given