```
```java
public int score() {
    int score = 0;
    int frameIndex = 0;
    for (int frame = 0; frame < 10; frame++) {
        if (isSpare(frameIndex)) {
            score += 10 + rolls[frameIndex + 2];
            frameIndex += 2;
        } else {
            score += rolls[frameIndex] + rolls[frameIndex + 1];
            frameIndex += 2;
        }
    }
    return score;
}
```
```

```
```java
private boolean isSpare(int frameIndex) {
    return rolls[frameIndex] + rolls[frameIndex + 1] == 10;
}
```
```

That’s better. We can also clean up the ugly comment in the spare test by doing the same:

Click here to view code image

```
```java
private void rollSpare() {
    rollMany(2, 5);
}
```
```

```
```java
@Test
public void oneSpare() throws Exception {
    rollSpare();
    g.roll(7);
    rollMany(17, 0);
    assertEquals(24, g.score());
}
```
```

Replacing comments with pleasant little functions like this is almost always a good idea. The folks who read your code later will thank you.

So, what’s the next test? I suppose we should try a strike:

Click here to view code image