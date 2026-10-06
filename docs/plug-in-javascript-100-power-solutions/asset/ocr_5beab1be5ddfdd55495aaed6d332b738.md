# Chapter 5: Visibility 109

# A Standard Formula

The preceding formula is how almost all the animations and transitions in this book work. They take the value in milliseconds that you supply for their duration, then they divide that by the interval (usually 30 milliseconds), and finally they find the distance between the start and end points of the animation by the timing value, to find out the amount animation needs to move on each step, as shown in the following statement:

```
var stepval = Math.abs(start - end) / (msecs / INTERVAL)
```

# If a Fade Is Already in Progress

This plug-in is designed so that you can force it to proceed until it has finished, or allow it to be interrupted (but only by Fade() call on the same object). This is so that you can offermouseover and mouseout routines that will interrupt if you move your mouse before the transition completes. That way, a partially faded object can be faded back to start point again if you take the mouse away.

Alternatively, you may need to display an uninterrupted animation on the screen and maybe even one fade. You have the option to choose either by setting the interruptible argument to true if a fade can be interrupted, or if it cannot. You can also use 1 and 0 for these values if you prefer.

The next section of code checks whether a fade is already in progress by looking at the FA_Flag property of id. This is a new property given to id, which has the value true only when fade is in progress.

> Note Assigning new properties to objects is a technique used throughout this book. It's a convenient way of using some object-oriented aspects of JavaScript.

The next section of code checks whether a fade is already in progress. If it is, the code checks whether the FA_Int property of id is set (to see whether an interrupt is allowed). If it isn't, the function immediately exits as it cannot interrupted. Otherwise, the clearInterval() function is called to end the repeating transitions, and the object's new FA_Start property is set to the current value in FA_Fade.

This primes the new fade to start where the previous one (which was just cancelled) left off, which means that the new fade will ignore the start value that was passed. This override ensures a very smooth and natural flow between the two transitions. The following code performs this:

```
if (O(id).FA_Flag)
{
  if (O(id).FA_Int) return

  clearInterval(O(id).FA_IID)
  O(id).FA_Start = O(id).FA_Level
}
```

# If a Fade Is Not in Progress

If a fade isn't already in progress, the new id property FA_Start is assigned the value in start so that the remaining code can use this to know where the fade started from.