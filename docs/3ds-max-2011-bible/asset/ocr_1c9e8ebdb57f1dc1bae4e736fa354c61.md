# FIGURE 21.1

The Time Configuration dialog box lets you set the number of frames to include in a scene.

![](bbox=[0.02, 0.25, 0.38, 0.58])

The Time Configuration dialog box also lets you specify the Start Time, End Time, Length, and Current Time values. These values are all interrelated, so setting the Length and the Start Time, for example, automatically changes the End Time. These values can be changed at any time without destroying any keys. For example, if you have an animation of 500 frames and you set the Start and End Time to 30 and 50, the Time Slider controls only those 21 frames. Keys before or after this time are still available and can be accessed by resetting the Start and End Time values to 0 and 500.

The Re-scale Time button fits all the keys into the active time segment by stretching or shrinking the number of frames between keys. You can use this feature to resize the animation to the number of frames defined by Start and End Time values.

The Key Steps group lets you set which key objects are navigated using key mode. If you select Use Track Bar, key mode moves through only the keys on the Track Bar. If you select the Selected Objects Only option, key mode jumps only to the keys for the currently selected object. You can also filter to move between Position, Rotation, and Scale keys. The Use Current Transform option locates only those keys that are the same as the current selected transform button.

# Using Time Tags

To the right of the Prompt Line is a field marked Add Time Tag. Clicking this field pops up a menu with options to Add or Edit a Time Tag. Time Tags can be set for each frame in the scene. Once set, the Time Tags are visible in the Time Tag field whenever that time is selected.

# Working with Keys

It isn't just a coincidence that the largest button in the entire Max interface has a key on it. Creating and working with keys is how animations are accomplished. Keys define a particular state of an object at a particular time. Animations are created as the object moves or changes between two different key states. Complex animations can be generated with only a handful of keys.