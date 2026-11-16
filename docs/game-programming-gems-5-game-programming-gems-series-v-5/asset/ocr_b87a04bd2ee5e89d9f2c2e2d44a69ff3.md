the three frustum tests fails, it fails also in the next frame. Consequently, in the next frame, the frustum must start checking by the test that previously failed. That will allow the frustum to potentially reject objects with just one test when the object doesnt change too much in the frustum (see Figure 1.6.10).

![](bbox=[0.396, 0.226, 0.768, 0.446])

FIGURE 1.6.10 Rearranging the test order with knowledge of the previous frame information potentially allows rejecting the object in the first test.

The plane coherency can be implemented in many ways. The simplest is to store a byte in the bounding object that keeps the test that fails in the previous frame. When the frustum checks the object, it starts with the test that the byte points to, and if it succeeds, it continues with the other two as usual.

# Checking Whether the Object Is Inside the AABB That Surrounds the Frustum

Determining intersection against an axis-align bounding box is almost always reduced to six comparisons, two for each axis. No expensive operations have to be performed, thus, it is incredibly fast compared to the usual frustum test. In the “Other Uses” section, a method to determine the AABB that surrounds the frustum was shown. That method is very proficient, and best of all, it only has to be called once per frame if the frustum changes.

If an object is known to be outside of the AABB that surrounds the frustum, it has to be also outside of the frustum (see Figure 1.6.11). Testing the object against the AABB is fast and allows rejecting the object just by doing simple comparisons. However, if the object is not completely outside, the usual test against the frustum is performed.