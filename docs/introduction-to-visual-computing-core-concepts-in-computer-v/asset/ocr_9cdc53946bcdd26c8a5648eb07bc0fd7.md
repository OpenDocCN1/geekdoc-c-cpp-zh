![](bbox=[0.18, 0.13, 0.82, 0.26])

Figure 14.19. This figure shows some results of bump mapping: Original object on the left, the bump image in the middle and the bump mapped object on the right.

We can now use this normal map to achieve the bump mapping using the following steps.

+   1. Define a local coordinate system at parameter (u, v) on a surface using its normal and tangent vectors.
+   2. Find the transformation from the global coordinate system to this local coordinate system.
+   3. Transform the light and view vectors to this local coordinate system.
+   4. Find the perturbed normal n(u, v).
+   5. Compute the lighting using the perturbed normal and the transformed light and view vectors.

![](bbox=[0.18, 0.6, 0.52, 0.75])

Figure 14.19 shows some results. Can you see what is missing? First, note that no bumps show up at the silhouette. This is because there is no real displacement of pixels and the silhouette where geometry is most easily visible fails to fool the eye. Also, since geometry is not changed, self shadowing effects are not visible giving the trick away.

Figure 14.20. This shows an example of displacement map of a sphere.

Another technique, more commonly called a displacement map actually perturbs the geometry from P to P′ guided by an image. In this case, microgeometry needs to be created and rendered, something that the bump-map avoids. With displacement map, therefore, we can see the bumps at the silhouettes, self-occlusions and self-shadowing. Figure 14.20 shows an example.