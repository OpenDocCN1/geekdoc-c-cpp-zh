![](bbox=[0.168, 0.092, 0.715, 0.423])

Figure 12.6 Character running through the game world

# # SUMMARY

This chapter provides a comprehensive overview of skeletal animation. In skeletal animation, a character has a rigid skeleton that animates, and vertices act like a skin that deforms with this skeleton. The skeleton contains a hierarchy of bones, and every bone except for the root has a parent bone.

The bind pose is the initial pose of the skeleton, prior to any animations. You can store a local transform for each bone in bind pose, which describes the position and orientation of a bone relative to its parent. A global transform instead describes the position and orientation of a bone relative to object space. You can convert a local