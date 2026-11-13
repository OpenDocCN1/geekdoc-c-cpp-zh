
an associative array that can be addressed by a unique name. With STL, this can be done for scalar attributes by using a `map<string, vector<float>>`, for example. Given an attribute name as a `string` (for example, “temperature”), the `map` class returns a reference to the corresponding `vector<float>` that stores the actual data, or null if there is no such attribute. Similar associative arrays can be constructed for every attribute type.

## 3.9 Advanced Data Representation

In the preceding sections, we have seen how to reconstruct piecewise constant and piecewise linear functions from sampled datasets, represented on grids with various cell types, using constant and linear basis functions. For the vast majority of data visualization applications, these representations are sufficient. However, there are situations when more advanced forms of data manipulation and representation are needed. In this section, first, we will describe the task of data resampling, which is used in the process of converting information between different types of datasets that have different sample points, cells, or basis functions (Section 3.9.1). Then we will describe the process of interpolating data provided as a set of scattered points, in case we do not have cell information (Section 3.9.2).

### 3.9.1 Data Resampling

In our height-plot visualization example in Chapter 2, we saw several instances of reconstructing functions from a sampled dataset. We used piecewise linear interpolation for the polygonal surface itself. We used piecewise constant interpolation for the flat shading and piecewise linear interpolation for the Gouraud shading, respectively. Finally, we used piecewise constant interpolation for the surface normals. We saw in Chapter 2 that we need normal values at the polygon vertices, the vertex normals, to do the Gouraud shading of the surface. However, piecewise constant normals, i.e., the polygon normals themselves, are discontinuous at the polygon vertices—actually, over the complete polygon edges—so we cannot use them as approximations for the vertex normals. How can we compute vertex normal values from the known polygon normals?

The answer to this question is provided by a more general operation on discrete datasets, called _resampling_. Consider a source dataset $\mathcal{D} = (\{p_i\}, \{c_i\}, \{f_i\}, \{\Phi_i\})$ and a target dataset $\mathcal{D}' = (\{p'_i\}, \{c'_i\}, \{f'_i\}, \{\Phi'_i\})$, which approximate both the same continuous function $f : D \to C$, but where the source grid $(\{p_i\}, \{c_i\})$ differs from the target grid $(\{p'_i\}, \{c'_i\})$. Resampling computes the

![](img/1274306e378c42ed8a0ad5669902d2a1_124_0.png)

Figure 3.18. Converting cell to vertex attributes. The vertex value \(f'_i\) equals \(\frac{A_1 f_1 + A_2 f_2}{A_1 + A_2}\), the area-weighted average of the cell values using vertex \(i\).

values \(f'_i\) of the target dataset as function of the values \(f_i\) of the source dataset. For simplicity, we assume that both datasets use the same set of basis functions \(\Phi_i\), although this is not a strict requirement.

Cell to vertex resampling. Let us now consider a common resampling operation in data visualization: converting cell attributes (\(f_i\)) to vertex attributes (\(f'_i\)). Cell attributes imply the use of constant basis functions \(\Phi_i\), as discussed in Section 3.2. Vertex attributes, in contrast, imply the use of higher-order basis functions, such as linear ones. On the other hand, we want the sample points of the target grid cells (which are the target grid vertices) to be identical to the source grid vertices for the two grids to match, as shown in Figure 3.18 for a one-dimensional grid.

A desirable property of resampling a function \(\bar{f}\) is that it should lead to a function \(\bar{f}'\) that is close to \(\bar{f}\) over the whole domain D. Mathematically, this can be expressed as

```
\(\int_{c'_i} (\bar{f}' - \bar{f})^2 ds \approx 0, \quad \forall \text{ cells } c'_i \in \mathcal{D}'.\) (3.41)
```

That is, the integrals of the original function \(\bar{f}\) and the resampled function \(\bar{f}'\) are equal over all cells \(c'_i\) of the target grid. Using the normality property of the basis functions (see Equation (3.5)), we obtain after some computations that

```
\(f'_i = \frac{\sum_{c_j \in \text{cells}(p_i)} A(c_j) f_j}{\sum_{c_j \in \text{cells}(p_i)} A(c_j)}, \quad (3.42)\)
```

where \(A(c_j)\) is the area of source grid cell \(c_j\) and \(cells(p_i)\) are all cells that have point \( p_i \) as vertex. In other words, vertex data is the area-weighted average of the cell data in the cells that use a given vertex. Equation (3.42) is identical to Equation (2.8) used in Section 2.2 to compute vertex normals for Gouraud shading from the polygon normals.

Vertex to cell resampling. Using similar reasoning, we can compute the conversion formula from vertex attributes (\( f_i \)) to cell attributes (\( f_i \)) as being

```
\( f_i = \frac{\sum_{P_j \in \text{points}(c_i)} f_j^{P_j}}{C}, \quad (3.43) \)
```

where points(\( c_i \)) denotes all points \( p_j \) that are vertices of cell \( c_i \) and \( C = |\text{points}(c_i)|\) is the number of vertices of cell \( c_i \). In other words, cell attributes are the average of the cell's vertex attributes.

In conclusion, we can always convert between cell attributes and vertex attributes. However, this does not mean that a dataset with cell attributes is identical to one with vertex attributes. As explained previously, cell attributes imply using piecewise constant interpolation, whereas vertex attributes imply a higher-order interpolation, such as linear. Resampling data from, e.g., cells to vertices increases the assumed continuity. If our original sampled data were indeed continuous of that order, no problem appears. However, if the original data contained, e.g., zero-order discontinuities, such as jumps or holes, resampling it to a higher-continuity grid also throws away discontinuities which might have been a feature of the data and not a sampling artifact. An example of this delicate problem is given in Section 9.4.7. In contrast, resampling from a higher continuity (e.g., vertex data) to a lower continuity (e.g., cell data) has fewer side effects—overall, the smoothness of the data decreases globally.

Subsampling and supersampling. Data resampling is not limited to converting between cell and vertex samples. Two other frequently used resampling operations are subsampling and supersampling. Subsampling is a resampling operation that reduces the number of sample points. Supersampling is useful when we are interested in optimizing the processing speed and memory demands of a visualization application by working with smaller datasets. In most cases, the subsampled dataset uses the same basis functions as the original dataset and its points are actually a subset of the original dataset points. However, this is not mandatory. After eliminating a certain number of sample points, subsampling operations can choose to redistribute the remaining points in order to obtain a better approximation of the original data in terms of the integral criterion defined earlier. Subsampling implementations can take advantage of the dataset topology. For example, on uniform, rectilinear, and structured grids, an often-used subsampling technique is to keep every kth point along every dimension and discard the remaining ones. This technique, called *uniform subsampling*, is simple to implement and quite effective when the original dataset is densely sampled with respect to the data variation. However, uniform subsampling makes no assumptions about the spatial data variation, so it might discard important features, such as regions where the data changes rapidly, together with less important, constant regions. Given the way most interpolation functions (such as constant and linear) reconstruct the data, a desirable property of subsampling is to keep most samples in the regions of rapid data variation and cull most samples from the regions of slow data variation. In Section 8.4, we shall present several subsampling methods applicable to both structured and unstructured datasets.

Supersampling (also called *refinement*) is the inverse of subsampling. Here, more sample points are created from an existing dataset. Similar to subsampling, the supersampled dataset usually includes all the original dataset points and uses the same basis functions, although this is not mandatory. Supersampling is useful in several situations when we need to manipulate or create information on a dataset at a level of detail, or scale, that is below the one captured by the sampling frequency, or density, of that dataset. In that case, we introduce more points by supersampling, and then use these to encode the desired detail information. The counterpart of uniform subsampling is *uniform supersampling*, which introduces k points into every cell of the original dataset. Similar to subsampling, an efficient supersampling implementation usually inserts extra points only in those spatial regions of the dataset where we need to further add extra information. We shall discuss several supersampling methods in Section 8.4.

### 3.9.2 Scattered Point Interpolation

So far, our definition of a sampled dataset has been based on a grid of cells that represent a tiling of the data domain (see Section 3.2). However, there are situations when we would like to avoid constructing or storing such a grid. Such a case occurs when you have measured some data at some given points that have a complex spatial distribution, and you have no explicit cell information that would connect the points into a tiling of some domain. A classical example is 3D surface scanning, where laser devices are used to measure the position of a set of points on the surface of a 3D object. For complex object surfaces, this process delivers a scattered 3D point set, also called a *point cloud*, with optional surface normal and surface color per-point attributes. Hence, all the data we have to work with are the points and their corresponding data values {p_i, f_i}.
