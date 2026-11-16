+   - Sprites
+   - XML model files
+   - Generic state framework
+   - Loading screen
+   - Attract mode with multiple screens
+   - Gameplay
+   - High score persistence

This is a lot of code to cover. Fortunately, the entire rest of the book goes into great detail about the inner workings of all these parts and pieces, so there isn't a lot of new information. In fact, other than the GameState and the GameController objects, everything should be familiar. All of the code is located in the javagames.completegame package, or other packages within this base package. The code listings all contain the package declaration, so you can always refer back to the code examples if you are having trouble finding the source.

Let's finish finding a game...

# THE BULLET CLASS

The Bullet class is the only previous class that remains unchanged (except for the package name).

```
package javagames.completegame.object;

import java.awt.Color;
import java.awt.Graphics2D;
import javagames.util.*;

public class Bullet {
    private Vector2f velocity;
    private Vector2f position;
    private Color color;
    private float radius;

    public Bullet( Vector2f position, float angle ) {
        this.position = position;
        velocity = Vector2f.polar( angle, 1.0f );
        radius = 0.06f;
        color = Color.GREEN;
    }
```