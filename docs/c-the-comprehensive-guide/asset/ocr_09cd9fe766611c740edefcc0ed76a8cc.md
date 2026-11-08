```
```
You have reached 700 points.
You have reached 800 points.
Space is empty after 82 shots. You have reached 1000 points.
You have reached 800 points.
You have reached 900 points.
```
```

As the program is set in `main()`, 10 asteroids are generated as targets on the game board. Each starts with ten “structure” points; when these reach zero, the asteroid is destroyed. The last line of `Ship::fireUpon()` checks this. This method is called by the main method of the `GameBoard::shipFires()` minigame. Because the game board manages the asteroids as data fields, it is responsible for removing a destroyed asteroid from the “universe.” This happens after the line with `ship.fireUpon()`: the method itself reports with the return value whether the asteroid was destroyed. If that is the case, the ship gets points, and the hit rock is removed from the vector with `asteroids_.erase()`.

Which of the available asteroids the ship shoots at is determined by a die roll. For this, there is the `rollDice()` helper function. With the two `min` and `max` parameters, you specify how many sides the die should have and what the smallest rolled number is. The die roll itself is done using `std::uniform_int_distribution<int> {min, max}`. If you were to pass 1 and 6 as `min` and `max`, you would have a six-sided die. Because `max` is always adjusted to the number of available asteroids, this “die” always has a different number of sides. Note that with `random_device`, you get true random numbers. However, because debugging with true random numbers is difficult, you can also use `default_random_engine` instead. Then you always get the same sequence of numbers that only looks random. This is useful for debugging.

Above all, you can see in this example that `GameBoard` stores all the asteroids in a `vector<shared_ptr>`. I chose `shared_ptr` here because a `Ship` should also point to an `Asteroid` in this vector. Thus, both “own” an asteroid. If the `GameBoard` removes an asteroid from its vector with `erase`, the `Ship` still has “its” last targeted asteroid in sight and can query information about it; this can be useful in a more complex game. However, if `Ship ship{}` targets the next asteroid in the next dice round, the ship's `shared_ptr` relinquishes ownership of the previous one. Either it is now removed if the vector of the `GameBoard` no longer owns it, or it remains if it is still present. All in all, this is very convenient: you only have to worry about very little and don't need to be concerned.

Due to these automatisms, it is sometimes said that `shared_ptr` operates like Java garbage collection, but this is not the case. Java circumvents the problem of unique ownership through garbage collection. In C++, however, `shared_ptr` ensures communal ownership, which is well-defined. Thus, handling `shared_ptr` can sometimes feel as comfortable as worry-free object management in Java. However, there are fundamental differences. Especially because can precisely determine the timing of resource release, `shared_ptr` in C++ has an advantage over garbage collection.