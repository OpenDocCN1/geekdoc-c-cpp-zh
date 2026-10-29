```
oldRt = fishObj.rotation.z_rotation
newRt = (in coordsys pathObj pathObj.rotation.z_rotation)

if ((random 1 100) > 85) then
(
    fishObj.rotation.z_rotation += (newRt - oldRt) *
    (random 0.5 1.5)
)
)
```

2. Save your script (File > Save), and then press Ctrl+E to evaluate the script again. This script is saved in the Chap 49 directory as FishPath2.ms. Make the Camera01 viewport active, and click Play Animation. Figure 49.16 shows another frame of the animation. As you can see, the fish is heading in the right direction this time, and the tail is flapping wildly.

# FIGURE 49.16

A tail-flapping fish that faces the right direction as it follows the path

![](bbox=[0.16, 0.52, 0.92, 0.79])

Okay, take a look at what changed. First, you added a variable to refer to the fish's tail, so that it is easy to change when you add another fish. Also, you accessed the bend modifier of the tail and set its axis to 0, which corresponds to the X-axis. (You can try other values to see that it really does change the axis parameter in the rollout.)