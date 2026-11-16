The RandomAsteroidExample code is as follows:

```
package javagames.prototype;

import java.awt.*;
import java.awt.event.KeyEvent;
import java.util.*;
import javagames.prototype.PrototypeAsteroid.Size;
import javagames.util.*;

public class RandomAsteroidExample extends SimpleFramework {
	private PrototypeAsteroidFactory factory;
	private ArrayList<PrototypeAsteroid> asteroids;
	private Random rand;

	public RandomAsteroidExample() {
		appBorderScale = 0.9f;
		appWidth = 640;
		appHeight = 640;
		appMaintainRatio = true;
		appSleep = 1L;
		appTitle = "Random Asteroids";
		appBackground = Color.WHITE;
		appFPSColor = Color.BLACK;
	}

	@Override
	protected void initialize() {
		super.initialize();

		rand = new Random();
		asteroids = new ArrayList<PrototypeAsteroid>();
		PolygonWrapper wrapper =
			new PolygonWrapper( appWidth, appWorldHeight );
		factory = new PrototypeAsteroidFactory( wrapper );
		createAsteroids();
	}

	private void createAsteroids() {
		asteroids.clear();
		for ( int i = 0; i < 42; ++i ) {
			asteroids.add( getRandomAsteroid() );
		}
	}

	private PrototypeAsteroid getRandomAsteroid() {
		float x = rand.nextFloat() * 2.0f - 1.0f;
		float y = rand.nextFloat() * 2.0f - 1.0f;
```