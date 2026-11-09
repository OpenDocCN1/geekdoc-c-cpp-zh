```
```java
@Test
public void oneStrike() throws Exception {
    g.roll(10); // strike
    g.roll(2);
    g.roll(3);
    rollMany(16, 0);
    assertEquals(20, g.score());
}
```
```

```
```java
public int score() {
    int score = 0;
    int frameIndex = 0;
    for (int frame = 0; frame < 10; frame++) {
        if (rolls[frameIndex] == 10) { // strike
            score += 10 + rolls[frameIndex+1] +
                     rolls[frameIndex+2];
            frameIndex++;
        }
        else if (isSpare(frameIndex)) {
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