# Part X: Dynamic Animation

You can execute this script by opening the Utilities panel, clicking the MAXScript button, and clicking the Run Script button. This opens a file dialog box. Locate the script and click Open, and the script runs. Running this script opens the Rag Doll dialog box, shown in Figure 43.11. Using this dialog box, you can provide a Name for the rag doll and set its Height and the number of Vertebra. The Create Humanoid button makes the rag doll appear in the viewports.

Once positioned, you can press the Constrain Humanoid button in the Constrain Humanoid rollout. This adds all the necessary constrains to the rag doll.

# Tip

You can use the rag doll script to place reactor constraints on a Biped object.

# FIGURE 43.11

Fully constrained humanoid figures can be created using the rctRagdollScript.ms script.

![](bbox=[0.09, 0.59, 0.32, 0.78])

The Point-to-Point constraint lets you attach two objects together by a common point. The attach point is the pivot point of the child and parent objects. It can be used to animate a lifeless body colliding with various rigid body objects. Using the Rag Doll constraint, you can manually define how the body joints can twist, rotate, and move.

# Tutorial: Swinging into a wall

Playing with the rag doll object is just plain fun. Remember that in the Preview window you can use the right-click button to throw the doll around. For this example, you use a couple of Point-to-Point Constraints along with a Rag Doll constraint to create a simple scene where the rag doll swings from a rope into a brick wall.

To animate a rag doll swinging on a rope, follow these steps:

+   1. Open the Swinging into a wall.max file from the Chap 43 directory on the DVD. This file includes a simple scene consisting of several Boxes, a Cylinder for the rope, and a brick wall.

+   2. Open the Utilities panel, and click the MAXScript button. Click the Run Script button in the MAXScript rollout. In the file dialog box, locate the Scripts directory where Max is installed. Select the rctRagdollScript.ms file, and click the Open button. The script file opens in a MAXScript window. In the MAXScript window, select the File→ Evaluate All menu command to make the Rag Doll panel appear.