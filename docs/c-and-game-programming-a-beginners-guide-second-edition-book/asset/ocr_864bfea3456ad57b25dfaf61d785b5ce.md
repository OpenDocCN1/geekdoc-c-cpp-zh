# Example 4.45. Patterns of movement for Battle Wave.

```
```java
public void MoveTargets(TimedEvent e, Object obj) {
    ...

    int newDirection = 0;
    Random rnd = new Random();

    if (targets[0].direction == AnimatedImage.SOUTH) {
        newDirection =
            (targets[0].imagePosX < targets[0].constraintBox.Width / 2) ?
                AnimatedImage.EAST : AnimatedImage.WEST;
    } else {
        for (int i = 0; i < NUM_TARGETS; i++) {
            if (!targets[i].isActive)
                continue;
            if (targets[i].imagePosX <= targets[0].constraintBox.X ||
                targets[i].imagePosX + targets[i].imageWidth >=
                    targets[0].constraintBox.X +
                    targets[0].constraintBox.Width) {
                newDirection = AnimatedImage.SOUTH;
                break;
            }
        }
    }

    for (int i = 0; i < NUM_TARGETS; i++) {
        if (newDirection != 0)
            targets[i].direction = newDirection;

        if (newDirection == AnimatedImage.SOUTH) {
            for (int j = 0; j < 5; j++)
                targets[i].Animate();
            if (targets[i].isActive && targets[i].imagePosY +
                targets[i].imageHeight >= player.imagePosY) {
                EndGame();
            }
        } else {
            targets[i].Animate();
            if (rnd.Next(100) > 85)
                if ((targets[i].direction == AnimatedImage.EAST &&
                     targets[i].imagePosX < player.imagePosX + 50 &&
                     targets[i].imagePosX > player.imagePosX) ||
                    (targets[i].direction == AnimatedImage.WEST &&
                     targets[i].imagePosX < player.imagePosX &&
```
```