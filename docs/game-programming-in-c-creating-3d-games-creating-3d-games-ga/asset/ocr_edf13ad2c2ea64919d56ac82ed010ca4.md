Ericson, Christer. Real-time Collision Detection. San Francisco: Morgan Kaufmann, 2005.

Millington, Ian. Game Physics Engine Development, 2nd edition. Boca Raton: CRC Press, 2010.

# EXERCISES

In this chapter's first exercise, you add jumping to the chapter's game project. In the second exercise, you improve upon the sweep-and-prune implementation covered in this chapter. In the last exercise you implement OBB versus OBB intersection between oriented bounding boxes.

# Exercise 10.1

Add jumping to the player character. The ground objects already have corresponding axis-aligned bounding boxes. To implement jumping, select a key (such as the spacebar). When the player presses the jump key, set an additional velocity in the positive z direction. Similarly, add a negative z acceleration for gravity that slows down the jump velocity. After the player hits the apex of the jump, he or she starts falling. While they player is falling, you can detect in FixCollisions whether the player lands on top of a PlaneActor (because you know that the top is dz2). While the player is on the ground, disable