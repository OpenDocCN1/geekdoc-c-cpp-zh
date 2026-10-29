# Motion Blur render effect

The Motion Blur effect applies a simple image motion blur to the rendered output. The Motion Blur Parameters rollout includes settings for working with Transparency and a value for the Duration of the blur. Objects that move rapidly within the scene are blurred.

# Depth of Field render effect

The Depth of Field effect enhances the sense of depth by blurring objects close to or far from the camera. The Pick Cam button in the Depth of Field Parameters rollout, shown in Figure 46.39, lets you select a camera in the viewport to use for this effect. Multiple cameras can be selected, and all selected cameras are displayed in the drop-down list. A Remove button lets you remove cameras.

# FIGURE 46.39

The Depth of Field Parameters rollout lets you select a camera or a Focal Point to apply the effect to.

![](bbox=[0.05, 0.57, 0.38, 0.82])

In the Focal Point section, the Pick Node button lets you select an object to use as the focal point. This object is where the camera focuses. Objects far from this object are blurred. These nodes are also listed in a drop-down list. You can remove objects from the list by selecting them and clicking the Remove button. The Use Camera option uses the camera's own settings to determine the focal point.

In the Focal Parameters section, if you select the Custom option, then you can specify values for the Horizontal and Vertical Focal Loss, the Focal Range, and the Focal Limit. The Loss values indicate how much blur occurs. The Focal Range is where the image starts to blur, and the Focal Limit is where the image stops blurring.

Figure 46.40 shows a beach scene created by Viewpoint Datalabs. For this figure, I applied the Depth of Field effect using the Pick Node button and selecting some leaves on the tree. Then I set the Focal Range to 100, the Focal Limit to 200, and the Focal Loss values to 10 for both the Horizontal and Vertical.

# Cross-Ref

The Depth of Field and Motion Blur effects can also be applied using a Multi-Pass camera, as discussed in Chapter 19, "Configuring and Aiming Cameras."