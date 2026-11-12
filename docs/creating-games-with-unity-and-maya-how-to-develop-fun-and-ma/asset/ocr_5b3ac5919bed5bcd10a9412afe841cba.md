**Step 7:** Repeat for additional sound source in the tunnel. Duplicate Sound-Waves in the Hierarchy window by selecting it, then right-click it and choose Duplicate. Rename the copy to Sound-Waves Tunnel and then move it into place (Figure 11.2).

![](bbox=[0.14, 0.201, 0.642, 0.424])

FIGURE 11.2 Additional wave source within the tunnel

> **Warnings and Pitfalls**
> When playing the game, it is possible to make changes to parameters of components (like Audio Sources) within the scene, and when these changes are made they will instantaneously be in effect. However, remember that these changes will revert once the game is stopped. So while tweaking things like volume while in-game are quick ways to find the right values, be sure to write these values down because they will need to be input again when the game is stopped.

> **Why?**
> The idea here is that the waves lapping against the side of the tunnel will create additional audio vibrations (sound). Placing an additional sound source here will ensure that this effect is heard.

**Step 8:** Test, test, test. When working with sound, testing often is critical and is really the only way to make sure that the settings work.

# Audio Reverb Zones

Audio Reverb Zones are areas of the model where effects are applied to the sounds that an Audio Listener is receiving. Audio Reverb Zones are fairly easy to place and are pretty handy in most simple situations. They simply create two spheres that define the effect of the reverb zone. The inner sphere indicates the area in which the reverb is in full effect, and the effect drops off to the volume of the outer sphere.

This works well, unless the zone is a cube (like the back of an enclosed truck). This can create goofy situations when walking around the outside of the truck can produce audio reverb effects as the player walks through the spheres that define the zone.

Still, in situations like ours, this will work fine since we don't need a terribly accurate zone (our zone will be the space under the covering).

**Step 9:** Create a new empty GameObject (GameObject>Create Empty). Place it in the back corner (where the entrance is). Name the GameObject Sound-ReverbZone.