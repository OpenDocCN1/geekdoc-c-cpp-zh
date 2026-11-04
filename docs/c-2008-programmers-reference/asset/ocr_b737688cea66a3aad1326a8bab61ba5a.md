# Part II: Application Development Using C#

A KeySpline is used to define the progress of an animation. The x-axis of the KeySpline represents time and the y-axis represents value. The KeySpline should now look like Figure 19-49.

![](bbox=[0.1, 0.22, 0.85, 0.58])

Figure 19-49

The modified KeySpline means “as time progresses, increase the rate of change.” In this example, it means that as the falling image approaches the bottom, it will drop faster.

Press F5 to test again, and you’ll see that the image accelerates as it nears the bottom. The animation is now more realistic, simulating free-fall.

# Playing Media

One of Silverlight’s key capabilities is a rich media experience. This section examines how to embed a Windows media file in your Silverlight application and how to control its playback. In addition, it also explains how to create simple effects on the video.

# Creating the Silverlight Project

Using Expression Blend 2, create a Silverlight project and name it Media.