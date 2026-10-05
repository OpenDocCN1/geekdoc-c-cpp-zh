animation, one shape would be tiny, another medium, another large. An explosion is a growing animation.

![](bbox=[0.306, 0.083, 0.597, 0.173])

# Animation Shapes by a Student

After you have created a shape, you'll notice a blank line beneath it where you can type in a name for it, for example pow1, pow2, or pow3. A name isn't necessary, though. After you save it, pause your mouse arrow over it to see how it is numbered. You can use either a name or a number to refer to it in the command setsh.

So you could say

+   - setsh [pow1 pow2 pow3]

or you could say

+   - setsh [35 36 37]

If your animation walks, set its heading so it moves to the side, and make it move forward by medium steps, like this:

+   - seth 90 repeat 100 [fd 3 wait 1]

If your animation grows, make it move forward by very tiny steps, one-hundredth of a step, written .01:

+   - seth 90 repeat 100 [fd .01 wait 1]

Remember, in an animation, first set your shapes, then move forward.

![](bbox=[0.342, 0.693, 0.597, 0.747])

# Explosion Shapes by a Student