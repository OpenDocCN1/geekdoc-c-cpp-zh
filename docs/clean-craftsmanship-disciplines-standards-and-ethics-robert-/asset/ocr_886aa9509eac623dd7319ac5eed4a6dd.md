```
```java
public void roll(int pins) {
    if (pins + lastPins == 10) { // horrors!
        //God knows what...
    }
    score += pins;
}
```
```

That `lastPins` variable must be a field of the Game class that remembers what the last roll was. And if the last roll and this roll add up to 10, then that’s a spare. Right? Ew!

You should feel your sphincter muscles tightening. You should feel your gorge rise and a tension headache beginning to build. The angst of the software craftsman should be raising your blood pressure.

*This is just wrong!*

We’ve all had that feeling before, haven’t we? The question is, what do you do about it?

Whenever you get that feeling that something is wrong, trust it! So, what is it that’s wrong?

There’s a design flaw. You might rightly wonder how there could be a design flaw in two executable lines of code. But the design flaw is there; it’s blatant, and it’s deeply harmful. As soon as I tell you what it is you’ll recognize it and agree with me. Can you find it?

*Jeopardy song interlude.*

I told you what the design flaw was at the very start. Which of the two functions in this class claims, *by its name*, to calculate the score? The score function, of course. Which function actually does calculate the score? The `roll` function. That’s misplaced responsibility.

> > ***Misplaced responsibility:*** *A design flaw in which the function that claims to perform a computation does not actually perform the computation. The computation is performed elsewhere.*

How many times have you gone to the function that claims to do some task, only to find that function does not do that task? And now you have no idea where, in the system, that task is actually done. Why does this happen?

Clever programmers. Or rather, programmers who *think* they are clever.