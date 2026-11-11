Not all file formats can handle multiple images. In that case, the `canInsertImage` method returns false for `i > 0`, and only a single image is saved.

The program in Listing 11.20 lets you load and save files in the formats for which the Java library supplies readers and writers. The program displays multiple images (see Figure 11.55), but not thumbnails.

![](bbox=[0.217, 0.262, 0.696, 0.628])

**Figure 11.55** An animated GIF image

# Listing 11.20 `imageIO/ImageIOFrame.java`

```
```java
package imageIO;

import java.awt.image.*;
import java.io.*;
import java.util.*;

import javax.imageio.*;
import javax.imageio.stream.*;

import javax.swing.*;
import javax.swing.filechooser.*;
```
```