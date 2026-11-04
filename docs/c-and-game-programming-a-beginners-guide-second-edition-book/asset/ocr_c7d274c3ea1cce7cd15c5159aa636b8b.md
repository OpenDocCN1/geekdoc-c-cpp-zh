pendent entities), and display and/or hide the asteroids, as necessary. We will use the OnPaint method to display introductory statements as well as some background stars and the sun. (see Example 3.50.) Asteroids are defined later in this chapter.

# Example 3.50. Space Fighter graphics.

```
```csharp
// Draw the scores
buffer.ColorFill(Color.Black);
buffer.ForeColor = Color.Red;
buffer.DrawText(4 * SCALE, 2 * SCALE, player1.score.ToString(), false);
buffer.ForeColor = Color.Blue;
buffer.DrawText(16 * SCALE, 2 * SCALE, player2.score.ToString(), false);

// Draw player 1 & its appropriate exhaust
try {
    destination = new Rectangle(player1.imagePosX, player1.imagePosY,
        SCALE, SCALE);
    buffer.Draw(destination, PlayerLDraw [player1.direction],
        DrawFlags.Wait);
} catch (SurfaceLostException) {
    CreateSurfaces ();
    ...
    if (plrVent.isActive) {
        try {
            int X = player1.imagePosX
                + exhaustImages[player1.direction].imageOffsetX;
            int Y = player1.imagePosY
                + exhaustImages[player1.direction].imageOffsetY;
            destination = new Rectangle(X, Y, SCALE / 2, SCALE / 2);
            buffer.Draw(destination, ExhaustDraw [player1.direction],
                DrawFlags.Wait);
        } catch (SurfaceLostException) {
            CreateSurfaces();
            ....
        }
    }
}
```
```

# Defining Hyperspace

Most of us see the world as a 4-dimensional platform, i.e., x, y, z, and time, and this serves us well in our daily lives. Yet, when working with the concept of space travel, we have to consider the possibility of moving through a fifth dimension, a.k.a. hyperspace. In