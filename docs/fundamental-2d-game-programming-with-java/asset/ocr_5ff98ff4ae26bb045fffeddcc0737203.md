```
long end = System.nanoTime();
averagedSpeed = (end - start) / 1.0E6; // convert to milliseconds
averagedSpeed /= 100;
```

The createTestImage() method is responsible for creating the test image used in the examples. The line spacing is specifically chosen to highlight the problems with some of the scaling methods. This is evident in the scaled results, where some of the vertical and horizontal lines are missing.

The render() method draws the original image and all the scaled versions, along with a label describing the rendering hint and the time in milliseconds to scale the image. The generateAverageInstance() and generateNearestNeighbor() methods scale the image using the getScaledInstance() method from the Image class. The scaleWithGraphics() method takes a rendering hint and scales the image using the Graphics object. Finally, the scaleDownImage() method steps down the scaled result gradually.

# Note

> The scaledDownImage() method is not a generic method for scaling an image. The scale-down size is hard-coded to one-fourth (¼) the size and the do/while loop will not work if the image is scaled to a larger size. That is covered in the next section.

```
package javagames.images;
import java.awt.*;
import java.awt.image.*;
import java.util.Hashtable;
import javagames.util.SimpleFramework;

public class ScaleImageExample extends SimpleFramework {
	private static final int IMG_WIDTH = 320;
	private static final int IMG_HEIGHT = 320;

	private BufferedImage sprite;

	private Image averaged;
	private double averagedSpeed;
	private Image nearestNeighbor;
	private double nearestSpeed;
	private BufferedImage nearest2;
	private double nearest2Speed;
	private BufferedImage bilinear;
	private double bilinearSpeed;
	private BufferedImage bicubic;
```