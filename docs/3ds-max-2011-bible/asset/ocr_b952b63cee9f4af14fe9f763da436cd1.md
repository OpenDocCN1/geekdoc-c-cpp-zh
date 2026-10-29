cles Start and Stop and the Amount or Rate. You can change these values by selecting the Birth event in the Event display and changing its parameters in the rollout that appears in the Parameters pane.

Several other default events appear in this default event node, including Position Icon, Speed, Rotation, Shape, and Display. Each of these events has parameters that you can alter that appear in the Parameters pane when the action is selected, and each event and action is identified with a number (such as 01) that appears next to its name. Each new event or action gets an incremented number. You also can rename any of these events if you right-click the event and select Rename from the pop-up menu.

A new Standard Flow can be created using the Edit > New > Particle System > Standard menu command. An Empty Flow includes only the PF Source node. When a new Standard Flow (or Empty Flow) is created in the Particle Flow window, a PF Source icon is added to the viewports. And if the PF Source icon is deleted in the viewports, the associated event nodes are also deleted in the Particle Flow window.

# Working with actions

The Depot pane includes all the different actions that can affect particles. These actions can be categorized into Birth actions (identified with green icons), Operator actions (identified with blue icons), Test actions (identified with yellow icons), and Miscellaneous actions (which are also blue). Each of these categories also can be found in the Edit > New menu.

New events can be dragged from the Depot pane to the Event display. If you place them within an existing node, a blue line appears at the location where the action will appear when dropped. The particles are affected within a node in the order, from top to bottom, in which they appear. If a new action from the Depot is dragged over the top of an existing action in the Event display, a red line appears on top of the existing action. When you drop the new action, it replaces the existing action.

Actions also can be dropped away from an event node, making it a new event node. If an event is a new node, then you can wire certain actions that are tested as true. For example, if you have a set of particles with a random speed assigned, then you could use a Test event to determine which particles are moving faster than a certain speed and wire those particles to change size using the new event node.

Clicking the action's icon disables the action.

# Tutorial: Creating an avalanche

One of the cautions that come with particles is that if you're not careful, you can quickly spawn enough particles to bring any system to its knees. Using the particle spawn feature is one of the worst offenders. For this tutorial, you use a Collision Spawn action to create an avalanche, but you must be sure to keep the number of spawned particles in check.

To use Particle Flow to make an avalanche effect, follow these steps:

+   1. Open the Avalanche.max file from the Chap 41 directory on the DVD.
+      This file includes a simple hillside covered with snow.
+   2. Select Create > Space Warps > Deflectors > SOmniFlect, and drag in the Top viewport to create a spherical deflector that covers the entire hill. Click the Select and Scale tool, and in the Z-axis, scale the SOmniFlect sphere down in the Left viewport until it is roughly the same thickness as the hill object. Then rotate the SOmniFlect until it is aligned parallel to the hill. This deflector is going to keep the snowball particles on top of the hill.
+   3. Select Create > Particles > Particle Flow Source, and drag in the Top viewport to create the emitter icon. Scale and rotate the emitter icon so it is positioned inside the SOmniFlect object on the uphill side pointing downhill. The emitter can be fairly small so it fits inside the deflector.