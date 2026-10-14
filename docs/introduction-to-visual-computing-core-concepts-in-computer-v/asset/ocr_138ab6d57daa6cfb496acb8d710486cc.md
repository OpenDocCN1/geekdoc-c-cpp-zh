where a and b are the two parameters of the shear matrix. It can be verified that the inverse of a shear matrix is

\(\mathcal{H}_z(a,b)^{-1} = \mathcal{H}_z(-a,-b).\)
(6.35)

# 6.3.5 Some Observations

This brings us to the end of the discussion on basic Euclidean and affine transformations. Here are a few observations from this discussion. First, since Euclidean transformations preserve lengths and angles, they will automatically preserve the ratio of lengths and angles. Therefore, *Euclidean transformations are a subset of affine transformations*. Euclidean transformations are often called *rigid body transformation* since the shape of the object cannot be changed by these transformations.

Next, all affine transformations of 3D space we have discussed have the last row predefined to be (0, 0, 0, 1). This is not a coincidence. Affine transformation in 3D can be represented as a linear transformation in 4D, and is a subspace of all 4D linear transformations. In other words, in affine transformation, we have the liberty to change only 12 parameters of the 4 × 4 matrix and still be in this subspace. This is often described as the degrees of freedom of a class of transformations. In other words, *affine transformations in 3D have 12 degrees of freedom*. However, it is a coincidence that for affine transformations the number of degrees of freedom is the same as the number of entries that can be changed in the matrix. We will have an in-depth discussion on the degrees of freedom at the end of this chapter.

Next, some points or lines are fixed under certain transformations i.e. they do not change position with the transformation. For example, the origin is fixed under scaling and shear in 3D. The axis of rotation is fixed under 3D rotation and the origin is fixed under 2D rotation. These are called *fixed points of mappings*. It can be seen that there are fixed points under translation.

Finally, the translation matrix cannot be expressed as a 3 × 3 matrix while scaling or rotation or shear can be. Homogeneous coordinates are essential to express translation in 3D as a linear transformation in 4D. This is another practical importance of having homogeneous coordinates.

# 6.4 Concatenation of Transformations

You now know all the basic affine transformations. The next step is how to use this basic knowledge to find the matrices for more complex transformations like scaling or rotation about an arbitrary axes. To achieve this, we need to learn how to concatenate transformations.