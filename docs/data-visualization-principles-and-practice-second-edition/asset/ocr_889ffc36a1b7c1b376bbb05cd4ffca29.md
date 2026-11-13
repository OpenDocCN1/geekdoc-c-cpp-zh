![](bbox=[0.075, 0.125, 0.785, 0.365])

Figure 8.1. (a) Brick extraction. (b) Selection of cells with scalar value above 50.

that has a uniform, structured, or rectilinear grid, we produce a new dataset that has the same grid type. In the target dataset, we copy all points, cells, and corresponding data attributes that fall within the specified brick extent. Note that when we use this definition of bricking, the extracted object extent is parallel with the dataset extent and not the coordinate axes, and the extracted brick contains only whole cells. Consider, for example, the case of the structured grids shown in Figure 3.10.

Figure 8.1(a) shows a brick extracted from a volumetric magnetic resonance imaging (MRI) scan of a human head. The dataset extent is shown by the wireframe and the brick surface is color-mapped with the scalar values at the respective points of the extracted brick.

# 8.1.2 Slicing in Structured Datasets

Slicing is a cutting operation that is very similar to bricking. Given a uniform, rectilinear, or structured grid, we define a slice as all grid points that have one of the structured integer coordinates n1, ..., nd equal. Extracting a slice can be seen as a bricking operation where the brick extent (m1, M1), ..., (md, Md) is equal to the grid extent for d - 1 of the dimensions, except for the slicing axis s, where ms = Ms. Slicing a d-dimensional dataset generates a d - 1 dimensional dataset. As explained in Chapter 3 where we introduced the geometrical and topological dimensions of a dataset, this means that slicing creates cells of a lower dimension, but whose vertices are points in the same three-dimensional space as