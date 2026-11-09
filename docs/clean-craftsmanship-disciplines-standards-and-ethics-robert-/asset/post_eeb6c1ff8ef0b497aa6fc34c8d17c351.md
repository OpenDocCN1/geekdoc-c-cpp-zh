
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

Convince yourself that this is correct. There’s the strike, the 2 bonus balls, and 16 gutter balls to fill up the remaining eight frames. The score is 15 in the first frame and 5 in the second. All the rest are 0 for a total of 20.

This test fails, of course. What do we have to do to make it pass?

[Click here to view code image](#)

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

This passes. Note that we increment frameIndex only by one. That’s because a strike has only one ball in a frame—and you were so worried about that, weren’t you?

This is a very good example of what happens when you get the design right. The rest of the code just starts trivially falling into place. Pay special attention to Rule 6, boys and girls, and get the design right early. It will save you immense amounts of time.

We can clean this up quite a bit. That ugly comment can be fixed by extracting an `isStrike` method. We can extract some of that ugly math into some pleasantly named functions too. When we’re done, it looks like this:

Click here to view code image

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

We can also clean up the ugly comment in the test by extracting a `rollStrike` method:

Click here to view code image

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

What’s the next test? We haven’t tested the tenth frame yet. But I’m starting to feel pretty good about this code. I think it’s time to break Rule 3 and go *for the gold*. Let’s test a perfect game!

Click here to view code image

```java
@Test
public void perfectGame() throws Exception {
    rollMany(12, 10);
    assertEquals(300, g.score());
}
```

We roll a strike in the first nine frames, and then a strike and two 10s in the tenth frame. The score, of course, is 300—everybody knows that.

What’s going to happen when I run this test? It should fail, right? But, no! It passes! It passes because we are done! The `score` function *is* the solution. You can prove that to yourself by reading it. Here, you follow along while I read it to you:

Click here to view code image

```text
For each of the ten frames
    If that frame is a strike,
        Then the score is 10 plus the strike bonus
            (the next two balls).
    If that frame is a spare,
        Then the score is 10 plus the spare bonus
            (the next ball).
    Otherwise,
        The score is the two balls in the frame.
```

*The code reads like the rules for scoring bowling. Go to the beginning of this chapter and read those rules again. Compare them to the code. And then ask yourself if you’ve ever seen requirements and code that are so closely aligned.*

Some of you may be confused about why this works. You look at the tenth frame on that scorecard and you see that it doesn’t look like any of the other frames; and yet there is no code in our solution that makes the tenth frame a special case. How can that be?

The answer is that the tenth frame is not special at all. It is drawn differently on the score card, but it is not scored differently. There is no special case for the tenth frame.

*And we were going to make a subclass out of it!*

Look back at that UML diagram. We could have divided out the tasks to three or four programmers and integrated a day or two later. And the tragedy is that we’d have gotten it working. We would have celebrated the 400<sup>6</sup> lines of working code, never knowing that the algorithm was a `for` loop and two `if` statements that fits into 14 lines of code.

6. I know it’s 400 lines of code because I’ve written it.

Did you see the solution early? Did you see the `for` loop and two `if` statements? Or did you expect one of the tests to eventually force me to write the `Frame` class? Were you holding out for the tenth frame? Is that where you thought all the complexity would be found?

Did you know we were done before we ran the tenth frame test? Or did you think there was a lot more to do? Isn’t it fascinating that we can write a test fully expecting more work ahead, only to find, to our surprise, that we are done?

Some folks have complained that if we’d followed the UML diagram shown earlier, we’d have wound up with code that was easier to change and maintain. That’s pure bollocks! What would you rather maintain, 400 lines of code in four classes or 14 lines with a `for` loop and two `if` statements?

## Conclusion

In this chapter, we studied the motivations and basics of TDD. If you’ve gotten this far, your head may be spinning. We covered a lot of ground. But not nearly enough. The next chapter goes significantly deeper into the topic of TDD, so you may wish to take a little rest before turning the page.

The last two examples in [Chapter 2](#), “Test-Driven Development,” begged an interesting question. Where does the algorithm that we derive using test-driven development (TDD) come from? Clearly it comes from our brain, but not in the way we are used to thinking. Somehow, the process of failing tests coaxes the algorithm out of our brain without the need to think it all through beforehand.

This raises the possibility that TDD may be a step-by-step, incremental procedure for deriving any algorithm for any problem. Think of it like solving a mathematical or geometric proof. You start from basic postulates—the degenerate failing tests. Then, one step at a time, you build up the solution to the problem.

At each step, the tests get more and more constraining and specific, but the production code gets more and more generic. This process continues until the production code is so general that you can’t think of any more tests that will fail. That solves the entire problem.

Let’s try this out. Let’s use the approach to derive an algorithm for sorting an array of integers.

If you can watch the video, this would be a good time, but in any case, please continue on to read the text that follows.

Watch related video: SORT 1

Access video by registering at [informit.com/register](https://informit.com/register)

We begin, as usual, with a test that does nothing:

[Click here to view code image](#)

```java
public class SortTest {
    @Test
    public void nothing() throws Exception {
    }
}
```

The first failing test will be the degenerate case of an empty array:

[Click here to view code image](#)

```java
public class SortTest {
    @Test
    public void sorted() throws Exception {
        assertEquals(asList(), sort(asList()));
    }
    private List<Integer> sort(List<Integer> list) {
        return null;
    }
}
```

This obviously fails, but it is easy to make it pass:

Click here to view code image

```java
private List<Integer> sort(List<Integer> list) {
    return new ArrayList<>();
}
```

Stepping up one level in degeneracy, we try a list with one integer in it:

Click here to view code image

```java
assertEquals(asList(1), sort(asList(1)));
```

This clearly fails, but we can make it pass by making the production code a bit more general:

Click here to view code image

```java
private List<Integer> sort(List<Integer> list) {
    return list;
}
```

Cute, right? And we saw that trick before, in the prime factors example in Chapter 2. It seems relatively common that the first two tests in a given problem are solved by returning the most degenerate answer, followed by the input argument.

The next test is trivial because it already passes: two elements in order. It could be argued that we shouldn’t even have written it because it’s not a failing test. But it’s nice to see these tests pass.

Click here to view code image

```java
assertEquals(asList(1, 2), sort(asList(1, 2)));
```

If we reverse the order of the input array, the test will fail: two elements out of order.
