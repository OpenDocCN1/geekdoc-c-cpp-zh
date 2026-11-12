
- **Step 26:** Turn off the trigger's Mesh Renderer components. Select each trigger in the Hierarchy and then in the Inspector panel, and click off Mesh Renderer. This will make the triggers disappear from view.

### Why?

They are no longer visible, but still functional. When we were building the mechanism it was handy to have the triggers visible because it made placement easier, and it made it easier to see when we actually had hit a trigger when playing the game. However, obviously we don't want these seen in the final game, so once we're confident that they are working, making them invisible is required.

- **Step 27:** Test again. Play the game to ensure the triggers are still working as planned.

## Triggers to Swap Levels

In the last chapter we used a GUITexture as a button that when clicked invoked the Application.LoadLevel process that exited Scene-Opening and entered Scene-EntryWay. Triggers are another nice way of doing this. As a player walks to a certain place in a level, Unity can exit that level and take the player to a new one.

Now, in today's games, this sort of Loading screen between levels is not as elegant as many other games. And in fact, Unity's new Occlusion Culling mechanisms would allow (in theory) for very large levels or even collections of levels to all be in one scene file. Occlusion Culling simply wouldn't draw the parts or levels that aren't seen (as opposed to the default behavior where Unity draws everything within the camera's frustum but just draws the things closest to the camera last). But Occlusion Culling is a Unity Pro feature and requires some careful construction of assets to begin with, so we're not going to get too far into this method. Instead we'll work with the old school scheme of having one Unity scene be the EntryWay and another be inside the base. If you plan to expand the game, you might consider other parts of the base as still further separate Unity scene files that are called up only when the character moves into that part of the facility.

For the next few steps it will be important to have the inside of the base available. These assets have been part of the Homework and Challenges of the past tutorials, but if you have not been doing those, they are also part of a package on the supporting web site (http://www.Creating3dGames.com). Be sure to grab those and import the package into your Unity project (Hallway_Chapter13-Start.unitypackage).

The results of the import will be a new Unity scene called Scene-Hallway. It should already be baked, but if the baking doesn't look right, you may need to fire the bake again. During the tech edit process we have found that some assets when moving between operating systems sometimes lose their lightmap connections.

### Why?

Just like in the last chapter, what this will do is that when the trigger is penetrated by another collider (like our First Person Controller), if the trigger's name is Trigger-HallwayPortal (which this trigger is), then the current level (Scene-EntryWay) will close as Scene-Hallway is loaded.

- **Step 32:** Save and return to Unity. Fix any syntax errors that pop up in the console.
- **Step 33:** If Scene-Hallway has not been added to the Scenes in Build section of the Build Settings, do so now (File->Build Settings).
- **Step 34:** To test this trigger, we will need to temporarily deactivate the doors. If you are using the version included on the web site (http://www.Creating3dGames.com) these are called EntryWayDoorGroup. If you're using your own, select the GameObject in the Hierarchy and turn it off in the Inspector (be sure to include the children when deactivating).

### Why?

When the game is actually finished, these doors will (of course) be active. The goal of this part of the game will be to use the EMP to short out the card reader that will open the doors. When the doors are open, the player can then walk into them where he would hit the trigger. The key is that we don't want the player to be able to hit this trigger before the doors are open so the trigger needs to be back behind the doors.

- **Step 35:** Test: walk through this trigger and see if you end up in the hallway.
- **Step 36:** If all's well, reactivate the doors.
- **Step 37:** Apply all the changes you've made to the First Person Controller prefab, so that it can be used elsewhere. Select First Person Controller in the Hierarchy, and in the Inspector press the Apply Button on the Prefab line. We want all the interface details to be included here in other levels. We'll discuss much more about prefabs later (Chapter 15).
- **Step 38:** Create a new prefab and name it GUIElements (remember to do this in the Project panel). Drag GUITextHints from the Hierarchy panel to this new GUIElements prefab in the Project panel (this populates the new prefab). Now, delete GUITextHints from the Project panel and drag GUIElements up to the Hierarchy. Finally, make sure that GUIElements' Transform Position XYZ are all set to 0 (this is done by selecting GUIElements in the Hierarchy and changing the values (if needed) in the Inspector).

### Why?

We've carefully arranged these GUITextHints to be at the bottom of the screen, and we've done this with the Transform Position settings. If the parent of the GUITextHints is not at 0,0,0 then Unity has to do some funny tweaking to the values of its children to get them in the same place as they were before being children. So taking just a second and making sure that empty parent objects are indeed at a position of 0,0,0 will help solve all sorts of problems later.

## Conclusion

So far we have used triggers to provide on-screen help via GUI Text. We've also used a trigger to transport us to a new level. Triggers can really be used to launch anything. In the next tutorial we will look at using a trigger to open a door automatically as we approach.

It's worth pointing out some of the limitations of this method and some alternatives. Our current method uses OnTriggerEnter and attaches the script to the actual trigger. Alternatively, Unity has a built-in function of OnControllerColliderHit that is built specifically for use with the First Person Controller (and should be applied to the First Person Controller). This can also do some great things and can help avoid situations where a trigger might be set off by other colliders moving within the scene. However, it requires a bit of extra theory that we haven't covered yet, and for this particular scene (that doesn't have other random colliders moving through the scene) the solution we've used is quick and easy.

## Tutorial 13.2: Triggers and Doors

Using triggers as automatic door openers can work well in simple situations. As the situation increases in sophistication (you need to have a key, or the door is opening toward you) there are some better methods dealing with Raycasting (more on this later). For instance, with the trigger solution we are using now, an opening door will open whether we are looking at it or not; using Raycasting we can mitigate problems like that. However, let us look at how triggers can be used in some simple situations.

For this tutorial we will be using the Scene-Hallway. There are loads of doors there that need to be opened. So, if you need this scene, be sure to download the package from the web site (http://www.Creating3DGames.com).

Once the Scene-Hallway (see step 1) is open, there are actually two versions of the hallway—one that is lit and baked (called Hallway_BakedGroup) and a second one called Hallway_Unbaked. When the scene is opened, Hallway_Unbaked will be deactivated. This is because it's dark—really dark—and pretty tough to work with. Although much of what we'll do here has to do with that version of the hallway, we'll set up our mechanics on the Hallway_Baked version for ease of use.

- **Step 1:** Open Scene-Hallway.
- **Step 2:** Reuse our First Person Controller prefab and the GUIElements prefab for this scene. Do this by dragging them from the Project panel up into the Hierarchy. Position the GUIElements to Transform Position (0,0,0). Maneuver the First Person Controller into position at the front of the scene.
