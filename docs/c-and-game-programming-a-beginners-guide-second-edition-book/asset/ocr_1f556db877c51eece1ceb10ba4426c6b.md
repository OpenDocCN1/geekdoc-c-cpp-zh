```
}
}
public void ItemPattern1(Graphics g, Brush bAlienColor,
    int current) {
    if(current >= 0 && current <= 4) {
        this.Alien0(g, bAlienColor);
    else if(current >= 5 && current <= 9) {
        this.Alien1(g, bAlienColor);
    else if(current >= 10 && current <= 14) {
        this.Alien2(g, bAlienColor);
    else if(current >= 15 && current <= 19) {
        this.Alien3(g, bAlienColor);
    }
}
}
}
```

# GameState.cs

GameState.cs contains the GameState class that is responsible for maintaining simple state information about a game such as the speed, state (started, stopped, etc.), and mode (demo, single player, etc.). The GameState class is an independent class, but it is a vital component of all the games constructed in this text (see Example 5.73 and GameState.cs on the CD-ROM).

# Example 5.73. GameState.cs

```
using System;

namespace GameClasses {
    public class GameState {
        // Different speeds the game can be run in.
        public const int SPEED_MINIMUM = 1;
        public const int SPEED_DEFAULT = 3;
        public const int SPEED_MAXIMUM = 10;
```