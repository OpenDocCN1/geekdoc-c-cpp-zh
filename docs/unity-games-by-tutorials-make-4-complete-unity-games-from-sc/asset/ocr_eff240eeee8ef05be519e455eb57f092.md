# Creating your first tower

Before creating any towers, you need a TowerSlot to place them on. Drag the TowerSlot prefab from the Prefabs ▸ Tower folder into the Hierarchy. Set its position to (-4, 0, 10).

![](bbox=[0.425, 0.211, 0.574, 0.319])

This is a quad with a texture on it and a Box Collider to allow interaction with it by clicking. Notice that there's an Event Trigger component attached. This handles all the events when the player's cursor enters and exits, and when a click happens as well.

# Stone tower

The first of the towers is the affordable and reliable Stone Tower.

![](bbox=[0.425, 0.492, 0.574, 0.725])

Drag the StoneTower prefab from the Prefabs ▸ Tower folder into the Hierarchy and change its position to (-1, 0, 10) so you can still see the TowerSlot.

Create a new folder Tower inside the Scripts ▸ Game folder. Create a new C# Script named Tower and open it in a code editor. At this point, you may be thinking "Wait a minute, I'm making the script for a Stone Tower here. Shouldn't the script be StoneTower?