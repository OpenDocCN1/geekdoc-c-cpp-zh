# Chapter 5: Visibility

# TheDoFade() Subfunction

This function is a subfunction of Fade () and is known as a private method or private function. Such functions share all the local variables of the parent function, so there's no need to pass them as arguments, and they can only be used by the parent function, they don't clutter the namespace.

This makes it ideal to use as interrupt or driven functions, which is exactly what I have done in this plug-in. Every INTERVAL milliseconds (30 by default), DoFade() is called by JavaScript. It has one main job, which is to change the opacity of id by just a little. The following line is the one that changes the value for this:

```
O(id).FA_Level += O(id).FA_Step
```

This simply adds the value of the FA_Step property of id to its FA_Level property. If FA_Step is positive, the value is therefore added, but if it is negative it is subtracted (for example 100 - 3 is 97, because the first + ignored)

# The Final Opacity Has Been Reached

Having derived this new value, it's time to check whether it is the final value wanted, and so the animation completes. The code to do is slightly verbose:

```
O(id).FA_Level >= Math.max(O(id).FA_Start, O(id).FA_End) ||
O(id).FA_Level <= Math.min(O(id).FA_Start, O(id).FA_End)
```

Essentially, it checks whether the current opacity (in FA_Level) has reached the final value (in FA_End). If it is as or greater (or less than, in the case of decreasing) the final value, then the following code segment is executed:

```
O(id).FA_Level = O(id).FA_End
O(id).FA_Flag = false
clearInterval(O(id).FAID)
```

In this section, the FA_Level is set to the exact value in FA_End. This must be done because FA_Level will often have a fractional value, and one final frame of animation is always required to ensure the correct opacity level is reached.

After this FA Flag property of id is set to false to indicate that the fade has finished. This is immediately followed by a call to clearInterval() with the value that was saved in the FA_ID property. This prevents any further interrupts.

# The CB Argument

The final statement in this if () section is as follows:

```
if (typeof CB != UNDEF) eval (CB)
```

It catches the argument passed in CB (if any) and uses the eval () function to evaluate it. This type of procedure is called a callback and is used by the chaining plug-ins. In a nutshell, now that this plug-in has completed running, this allows any plug-ins to chain to begin their execution. However, this happens only if the argument CB has a value.