# FIGURE 39.17

CAT muscles provide a way to simulate flatter rows of muscles.

![](bbox=[0.08, 0.24, 0.85, 0.62])

# Tutorial: Adding muscles to a rig

In this example, you take the default human character rig and add a CAT muscle to the front for the chest and stomach definition.

To add muscles to a rig, follow these steps:

+   1. Open the Human char with muscles.max file from the Chap 39 directory on the DVD. This file includes the default CAT human rig.

+   2. Open the Create panel and choose the Helpers category and the CAT Objects subcategory. Click the CAT Muscle button and drag in the Front viewport to create a CAT muscle that runs from the collar bone to the pelvis on the left side. Then move the muscle plane into position in front of the ribcage bone.

+   3. Open the Modify panel and set the U and V Segs values to 15. Select and move the outer corners and their adjacent handles to make the muscles bend around the side of the body.

+   4. Select Create→ Extended Primitives→ Chamfer Box menu and drag to create a box with rounded corners. Then create and elongate a sphere object with the Create→ Standard Primitives→ Sphere menu. Position the rounded box at the location of the pectoral muscle. Position and clone the sphere to show three rows of stomach muscles.

+   5. Select the CAT muscle object, and in the Modify panel click the Add button for the Collision Detection section and select the rounded box and sphere objects. Then move the collision objects to create the desired muscle look in the CAT muscle.