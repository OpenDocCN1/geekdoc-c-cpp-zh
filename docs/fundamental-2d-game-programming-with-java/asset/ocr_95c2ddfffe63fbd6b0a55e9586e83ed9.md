Don't forget that you can get the full source code on the book's website at http://www.indiegameprogramming.com.

# THE ASTEROIDFACTORY CLASS

The AsteroidFactory class has been updated to parse an XML file to create the asteroids instead of using hard-coded values. This way, you can use the files created by the Swing GUI in Chapter 16, “Tools.” The XML format is as follows:

```
<?xml version="1.0"?>
<models>
    <model bounds="0.5859375" size="Large" sprite="large0.png">
        <coord x="-0.029733956" y="0.283255100" />
        <coord x="-0.183098610" y="-0.111111104" />
    </model>
</models>
```

The base model file comes from saving the XML file from the polygon editor. The models saved from the editor were just pasted into this file, and the size and sprite image were added. Either importing an image and drawing the polygon shape, or exporting the polygon shape and filling it with a sprite will work for creating the rock sprites and model file. If you want, you can grab the sprites and model files from the download section of the book’s website.

```
package javagames.completegame.object;

import java.awt.image.BufferedImage;
import java.io.InputStream;
import java.util.*;

import javagames.completegame.object.Asteroid.Size;
import javagames.util.*;

import javax.imageio.ImageIO;
import org.w3c.dom.Element;

public class AsteroidFactory {
    private Vector<Asteroid> small;
    private Vector<Asteroid> medium;
    private Vector<Asteroid> large;

    private float worldWidth;
    private PolygonWrapper wrapper;
    private Random rand;
```