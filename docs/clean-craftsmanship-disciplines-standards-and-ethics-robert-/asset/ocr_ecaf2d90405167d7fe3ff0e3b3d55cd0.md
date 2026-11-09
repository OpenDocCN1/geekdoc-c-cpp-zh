attention to Rule 6, boys and girls, and get the design right early. It will save you immense amounts of time.

We can clean this up quite a bit. That ugly comment can be fixed by extracting an `isStrike` method. We can extract some of that ugly math into some pleasantly named functions too. When we’re done, it looks like this:

Click here to view code image

```
```java
public int score() {
  int score = 0;
  int frameIndex = 0;
  for (int frame = 0; frame < 10; frame++) {
    if (isStrike(frameIndex)) {
      score += 10 + strikeBonus(frameIndex);
      frameIndex++;
    } else if (isSpare(frameIndex)) {
      score += 10 + spareBonus(frameIndex);
      frameIndex += 2;
    } else {
      score += twoBallsInFrame(frameIndex);
      frameIndex += 2;
    }
  }
  return score;
}
```
```

We can also clean up the ugly comment in the test by extracting a `rollStrike` method:

Click here to view code image

```
```java
@Test
public void oneStrike() throws Exception {
  rollStrike();
  g.roll(2);
  g.roll(3);
  rollMany(16, 0);
  assertEquals(20, g.score());
}
```
```

What’s the next test? We haven’t tested the tenth frame yet. But I’m starting to feel pretty good about this code. I think it’s time to break Rule 3 and go *for the gold*. Let’s test a perfect game!