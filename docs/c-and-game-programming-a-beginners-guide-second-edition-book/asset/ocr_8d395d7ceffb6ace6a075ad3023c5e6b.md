```
```csharp
if(-400 < JState.X) {
    playerR.direction = AnimatedImage.WEST;
    Joystick = true;
}
else if(-500 > JState.X) {
    playerR.direction = AnimatedImage.EAST;
    Joystick = true;
}

if(-600 > JState.Y) {
    playerR.direction = AnimatedImage.SOUTH;
    Joystick = true;
}
else if(-500 < JState.Y) {
    playerR.direction = AnimatedImage.NORTH;
    Joystick = true;
}
. . . .

if(theBall.isActive == false && gameState.currentState !=
    GameState.State.Stopped) {
    byte[] buttons = JState.GetButtons();
    foreach (byte b in buttons) {
        if (0 != (b & 0x80)) {
            Serve ();
        }
    }
}
. . . .
```
```

# Introducing Menus

Another interesting feature available to us as Visual C# programmers is the ability to create a host of menus both visually and through basic text references. The visual method, while straightforward, is not always as complete as the text-based method, hence the need to understand both techniques. Our first look will be at how to create a basic visual menu (this technique also applies to labels, buttons, boxes, pictures, etc.). First, we’ll need to reference our design window (Forms.cs [Design]). Next, we’ll need to reference the toolbox menu (located to the left side of our screen) and choose the appropriate interface (in this case, the Main Menu). From there we’ll simply drag and drop that selection onto our grid. (See Screen Shots 3.13 and 3.14).