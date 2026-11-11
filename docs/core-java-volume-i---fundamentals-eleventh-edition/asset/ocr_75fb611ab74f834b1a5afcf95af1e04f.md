a good idea—just in case a user of your program needs to select a file with a nonstandard extension. However, if you want to suppress the “All files” filter, call

```
chooser.setAcceptAllFileFilterUsed(false)
```

> > **CAUTION:** If you reuse a single file chooser for loading and saving different file types, call
> >
> > `chooser.resetChoosableFilters()`
> >
> > to clear any old file filters before adding new ones.

Finally, you can customize the file chooser by providing special icons and file descriptions for each file type that the file chooser displays. Do this by supplying an object of a class extending the FileView class in the javax.swing.filechooser package. This is definitely an advanced technique. Normally, you don’t need to supply a file view—the pluggable look-and-feel supplies one for you. But if you want to show different icons for special file types, you can install your own file view. You need to extend the FileView class and implement five methods:

```
Icon getIcon(File f)
String getName(File f)
String getDescription(File f)
String getTypeDescription(File f)
Boolean isTraversable(File f)
```

Then, use the setFileView method to install your file view into the file chooser.

The file chooser calls your methods for each file or directory that it wants to display. If your method returns null for the icon, name, or description, the file chooser then consults the default file view of the look-and-feel. That is good, because it means you need to deal only with the file types for which you want to do something different.

The file chooser calls the isTraversable method to decide whether to open a directory when a user clicks on it. Note that this method returns a Boolean object, not a boolean value! This seems weird, but it is actually convenient—if you aren’t interested in deviating from the default file view, just return null. The file chooser will then consult the default file view. In other words, the method returns a Boolean to let you choose among three options: true (Boolean.TRUE), false (Boolean.FALSE), or don’t care (null).