# Chapter 5: Visibility 123

Or, one button can hide another, like this:

```
<input id='a' type='submit' value='Button A ' onclick='Hide('b')' />
<input id='b' type='submit' value='Button B ' onclick='Hide('a')' />
```

The two lines each hide the other, so whichever is clicked first will stay displayed, the other button will not be hidden and therefore can't be clicked.
In the following plug-in you will see how Hide() can be combined with Show() for creating dynamic web page interaction.

# The Plug-in

```
{
S(id, 'display', 'none')
(id, 'HI_Flag', true)
if (typeof CB != UNDEF) eval (CB)
```

![](bbox=[0.047, 0.413, 0.235, 0.453])

This is the plug-in for Hide(). With it you can reveal an object that has previously been hidden. In Figure 5-14 the two plug-ins have been combined to create a mouseover menu of limericks.

# About the Plug-in

This plug-in will show an object, restoring its dimensions and location and moving back any elements that have moved in its space. It requires the following argument:

+   * An object, an object ID, or an array of objects and/or object IDs

![](bbox=[0.226, 0.627, 0.774, 0.903])

FIGURE 5-14 Different limericks appear as the mouse passes each heading.