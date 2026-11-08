Several dots on it (the keys in the graph part of the Graph Editor). Of all the key positions, the only three that we need are those at frames 1, 30 and 100. So, delete keys 1, 19, 39, 47, 53, 61, 69 and 75. You can do this by selecting the relevant dots on the animation curve in the Graph Editor and pressing Delete on your keyboard, or by selecting the keys in the Time Slider with the right mouse button and choosing delete. You should now have an animation curve that has three keys on it. In the Graph Editor select the key at frame 29. In the two Stats boxes at the top of the Graph Editor will be the numbers “9” (for frame 29) and “1” (for value of 1). Change the value from 1 to 0. This will make this key’s position drop down to 0 on the graph. When the visibility value of the ball is at 1 we can see it; when the visibility is at 0 we can’t! Repeat this procedure for the key at frame 100. Because you selected stepped keys earlier, the animation curve has a sharp ‘stepped’ look.

![](bbox=[0.074, 0.281, 0.903, 0.649])

We need to do the same thing for the ball attached to your man’s hand, but now the ball should be invisible from frames 1 to 28 then visible from frames 29 to 100. All you have to do is delete the irrelevant keys and make the value of the key at frame 100 0.

Make a Playblast of the animation to view it at the correct speed. It should look something like “lift_3D_keys.avi”, a 3D version of your 2D keys line test.

# Setting the Breakdowns in Maya

Go to frame 1 of your animation in Maya and take out drawings 1 to 9 of your drawn animation. The breakdowns (the major in-betweens) for this section are on frames 3 and 5. The timing chart for the in-betweens between these two keys shows that drawing 3 is one third closer to drawing 1 and two thirds further away from drawing 1 (see the earlier illustration on the timing chart). We need to move your man into this position on frame 3.