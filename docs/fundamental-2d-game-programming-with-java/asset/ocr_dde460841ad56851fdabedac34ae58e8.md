![](bbox=[0.098, 0.092, 0.603, 0.468])

Figure 16.1 Polygon Editor. © 2014 Timothy Wright.

The first step to updating the PolygonEditor, located in the javagames.tools package and shown in Figure 16.1, is to create a FileFilter class used to filter files from both save and load file dialogs. The following ExampleFileFilter extends Swing's FileFilter, adding a description and a method to filter out unwanted files by the file extension. By passing in a description and list of approved extensions, only approved files will be visible.

```
```java
package javagames.tools;

import java.io.File;
import javax.swing.filechooser.FileFilter;
```
```

```
```java
public class ExampleFileFilter extends FileFilter {
    private String description;
    private String[] filters;
```
```