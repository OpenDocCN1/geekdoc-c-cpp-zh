The last part of the RacePlayerController class overrides what happens when the vehicle hits a trigger, to add the extra functionality of respawn zones. A respawn zone is a trigger that will force an instant respawn of the player. For this to work, there needs to be a specific collision layer set up in Unity and respawnerLayerMask should be set to it in the Inspector on this component (on the prefab).

OnTriggerEnter() is a built-in Unity function, called by the engine for us and passing in the Collider this object hit as a parameter. Here, we named the Collider other.

To run the code from the original RaceController class that this one derives from, we then call base.OnTriggerEnter() and pass other as a parameter - effectively taking what got passed into this function and passing it on to the base class version.

The ExtendedCustomMonoBehaviour class provides a function named IsInLayerMask(), which can be used to find out if a layer falls within a LayerMask. To use it, you pass in the layer you want to check as the first parameter and the LayerMask as the second. Above, we pass in the Collider's GameObject's layer to look for and the respawnerLayerMask Layer as the LayerMask to look at.

When we know that the layer is the right one for a respawner, the code within the conditions curly brackets calls Respawn() to take care of respawning the vehicle.

# ### 14.4.5 Audio

For the vehicle audio in this game, we use a set of GameObjects with AudioSource Components attached to them. These GameObjects are child objects of the vehicle, moving around with the vehicle wherever it goes and activated to play by other scripts. For incidental sounds, a BaseSoundController Component holds an array of sounds such as bleeps during the countdown that can be played from other scripts.

# #### 14.4.5.1 Vehicle Audio

Vehicle audio is controlled by the following classes:

+   - WheeledVehicleController – The engine audio has its pitch controlled by this class. The engine audio is made up of a single sound loop which is played by an AudioSource Component attached to a GameObject named Engine, a child of the Vehicle_Player prefab.
+   - CrashSound – This Component takes an AudioSource (attached to a CrashSound GameObject on the player prefab in this game) and plays it at different volumes depending on the severity of impact, whenever the impact magnitude is greater than a value set in the Inspector. The magnitudeToPlay variable decides the minimum magnitude for an impact sound. The pitch is also randomized slightly to make the impact sounds more varied.

How the WheeledVehicleController deals with sound was outlined in Chapter 6, Section 6.2, during the breakdown of this script.

# #### 14.4.5.2 Incidental Sounds

Incidental sounds are controlled by a single BaseSoundController Component attached to the GameManager GameObject in the core Scene. You can find a full breakdown of the BaseSoundController in Chapter 9, Section 9.2.