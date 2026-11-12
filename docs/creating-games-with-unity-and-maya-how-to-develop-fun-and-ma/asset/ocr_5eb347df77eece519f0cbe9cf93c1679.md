# Why?

This might seem like a blast from the distant past, but when we were baking lighting, we marked objects or entire levels as Static. If an object is not marked as Static it won't be included in the baking. However, if it is marked as Static, Unity assumes that it's unmoving, that it's, well, static. Luckily, an object can be marked as Static and used in baking, but be dynamic later (as in this case) by just turning the Static option off after baking.

+   - **Step 13:** Test. Play the game and walk through that trigger and see if the timing is good. If the values of how far the door opens or the timing is not to your liking, adjust in the script.
+   - **Step 14:** Turn off the Mesh Renderer for the trigger Trigger-BulkheadDoor1.

# Sound and Scripts

The door should now open for us as we approach, but it's fairly creepy (and unrealistic) that it produces no sound as this door in an old sealed-up base opens. In this section we will add sound to the door and trigger it with our already extant script.

+   - **Step 15:** On the web, track down a sound clip that you think would be appropriate for this big door. I used “elevator door opening.wav” from FreeSound.org. Edit any unnecessary dead noise at the beginning or end of the sound (Audacity will do this quickly if you haven't any other sound application).
+   - **Step 16:** Import it to your Sounds folder by dragging it there in the operating system.
+   - **Step 17:** Create an empty GameObject (GameObject>Create Empty). Name it Sound-DoorOpenBulkhead1. Position it near where the opening door is. Drag the sound clip from the Project panel to this GameObject so that it contains an Audio Source component.

# Why?

Potentially this could also be attached to the character, but by actually placing it near where the sound would be emitting, we get the benefits of Unity's positionally aware sound system.

+   - **Step 18:** Turn off the Play on Awake option within the Audio Source component.

# Why?

By not playing on awake, the audio source stays silent until we ask it to play sound (which we will do in just a bit).