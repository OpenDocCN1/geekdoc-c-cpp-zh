![](bbox=[0.15, 0.15, 0.78, 0.32])

Figure 11.20. From left: One of the input images; the recovered surface normals encoded by a RGB vector; the surface albedo; the recontructed depth where depth is inversely proportional to the gray value; the same object relighted from a different virtual direction.

the total number of all such constraints is C. The value of C would have been 2PQ but for the pixels in the boundary for whom only one such constraint can be designed. Therefore, C < 2PQ but still sufficiently larger than PQ to create an over-constrained system of equations given by

M Z = B
(11.21)

where M is a C × PQ matrix whose entries can be either 1 or −1, Z is a PQ × 1 column vector containing the unknown depth and B is a same sized column vector of known scalar values. Therefore, Z can now be solved using a linear regression or singular value decomposition. The reconstructed depth is shown in Figure 11.18.

There are a few things to note from the above equations. We need to solve for three unknowns. Therefore, we need at least three lights (i.e. n = 3) to find the shape of the object. However, if the light directions are coplanar, L is rank-deficient and hence cannot be solved. Hence, we need at least three non-coplanar light directions. Other assumptions include that the camera image plane is parallel to the XY plane in the global coordinate system and the camera and the lights are distant from the object. Figure 11.19 shows that photometric stereo can give accurate surface normals but the recovered depth is inaccurate if the camera or the lights are placed very close to the object. Note that we do not need to find any correspondence unlike most stereo methods we have studied in Chapter 8 since the camera location does not change. Before processing the images in photometric stereo you have to undo the effect of the camera transfer function. Finally, once the surface normals and reflectance are computed, the object can be relighted from a light direction that was not available originally, as shown in Figure 11.20