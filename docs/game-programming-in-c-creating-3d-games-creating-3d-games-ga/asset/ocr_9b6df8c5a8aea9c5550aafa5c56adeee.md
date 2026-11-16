```
mc->SetForwardSpeed(150.0f);
}
```

One other new item in this `Asteroid` constructor is the use of the `Random` static functions. The implementation of these functions isn't particularly interesting: They simply wrap the built-in C++ random number generators to get a vector or float within a range of values. The `Random` functions here make sure that each asteroid gets a random position and orientation.

With this `Asteroid` class, you can then create several asteroids in the `Game::LoadData` function by using the following code:

Click here to view code image

```
const int numAsteroids = 20;
for (int i = 0; i < numAsteroids; i++)
{
    new Asteroid(this);
}
```

This results in several moving asteroids onscreen (see Figure 3.11).