variable that's only accessible in this function called `textureColor` that is of type `Color`. Then use a sin curve (looks kind of like a sound wave if it's been too long since your last math class that has gentle slopes up and gentle slopes down) to define the red value of the `textureColor` `Color`. This sin curve means that the red value is slowly being turned up, and then slowly turned down. Then, use the `textureColor` to define the color of the LED (`renderer.material.color`). `yield;` just means “wait” and keeps the looping function from being an infinite loop and crashing Unity.

**Step 14:** Save and return to Unity. Fix any syntax problems.

**Step 15:** Test. When the camera sees the player we should have a flashing LED.

# ## Adding Sound

**Step 16:** Find an alarm sound you like (I'm using `alarms.wav` from FreeSound.org; http://www.freesound.org/samplesViewSingle.php?id=54048). Download it and place within the Unity project file.

**Step 17:** On any `CCTV_Camera` prefab in the scene, select the LED (`Hallway_CCTV_Led`) and add an Audio Source component (`Component > Audio > Audio Source`). Place the alarm sound in the Audio Clip input field (either use target icon or drag and drop from Project panel). Turn off the Audio Source component, but make sure Play On Awake and Loop are both checked (Figure 15.10).

![](bbox=[0.142, 0.574, 0.637, 0.824])

**FIGURE 15.10** Settings for the CCTV camera.

> > **Why?**
> >
> > We don't want this sound to always be playing; we want to trigger it in the script (which is why we're turning off the Audio Source component), but once it does awake (and thus play) we want it to loop.