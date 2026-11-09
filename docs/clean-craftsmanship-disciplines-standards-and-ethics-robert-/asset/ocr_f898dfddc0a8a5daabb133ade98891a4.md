![](bbox=[0.128, 0.089, 0.833, 0.387])

**Figure 2.5 A UML diagram of the scoring of bowling**

The `Game` has ten `Frames`. Each `Frame` has one or two `Rolls`, except the `TenthFrame` subclass, which inherits the `1..2` and adds one more roll to make it `2..3`. Each `Frame` object points to the next `Frame` so that the `score` function can look ahead in case it has to score a spare or a strike.

The `Game` has two functions. The `roll` function is called every time the player rolls a ball, and it is passed the number of pins the player knocked down. The `score` function is called once all the balls are rolled, and it returns the score for the entire game.

That's a nice, simple object-oriented model. It ought to be pretty easy to code. Indeed, given a team of four people, we could divide the work into the four classes and then meet a day or so later to integrate them and get them working.

Or, we could use TDD. If you can watch the video, you should do that now. In any case, please read through the text that follows.

Watch related video: Bowling Game

Access video by registering at [informit.com/register](http://informit.com/register)