
### 9.11.2 Rendering Techniques

Rendering is the process of generating images using computers. In data visualization, our goal is to transform numerical data into graphical data, or graphical primitives, for rendering.

Traditional techniques assumed that when an object was rendered, the surfaces and their interactions with light were viewed. However, common objects such as clouds and fog are translucent and scatter light that passes through them. Therefore, for proper rendering, we need to consider the changing properties inside the object.

When we render an object using surface rendering techniques, we mathematically model the object with a surface description such as points, lines, triangles, polygons, or surface splines. The interior of the object is not described or is only implicitly represented by the surface representation.

One of the key developments in volume visualization of scalar data was the marching cubes algorithm of Lorensen and Cline [24]. The basic assumption of this technique and its higher-dimensional counterparts is that a contour can pass through a cell in only a finite number of ways. A case table is constructed that enumerates all possible topological states of a cell, given combinations of scalar values at the cell points. The number of topological states depends on the number of cell vertices, and the number of inside/outside relationships a vertex can have with respect to the contour value. A vertex is considered to be inside a contour if its scalar value is larger than the scalar value of the contour line. Vertices with scalar values less than the contour value are said to be outside the contour. For example, if a cell has four vertices and each vertex can be either outside or inside the contour, there are 2^4 = 16 possible ways that contour lines can pass through the cell. There are 16 combinations for a square cell, but these can be reduced to four cases by using symmetry (Figure 9.40). Once the proper case is selected, the location of the contour-cell edge intersection can be calculated using interpolation. The algorithm processes a cell and then moves or marches to the next cell. After all cells are visited, the contour will be complete. (Note: The dotted line in Figure 9.40 indicates a contouring ambiguity.)

**FIGURE 9.40:** Inside/outside relationship of a square whose vertices have numerical value either higher or lower than a set threshold.

![](img/f73ae67732328dc36596b27ffe8d0152_508_0.png)

○ = Less than iso-value of interest
● = Greater than iso-value of interest

In summary, the marching algorithm proceeds as follows:

- 1. Select a cell.
- 2. Calculate the inside/outside state of each vertex of the cell.
- 3. Create an index by storing the binary state of each vertex in a separate bit.
- 4. Use the index to look up the topological state of the cell in a case table.
- 5. Calculate the contour locations for each edge in the case table.

### 9.11.3 Region of Interest

Due to the localized nature of wavelets in frequency and space domains, Region of Interest refinement can be achieved by adding details in only the regions required. Figure 9.41 shows the ROI in the original image and in the wavelet domain for two levels of decomposition. Thus wavelets can be useful tool for compression as the image can be approximated by first reconstructing the low-pass coefficients and the detail can be restored to the ROI solely by transmitting the appropriate high-pass coefficients in the ROI. The results of this volume rendering using a 3D wavelet algorithm are shown in Figures 9.42-9.44.

**FIGURE 9.41:** The Region of Interest (ROI) (a) in the original image and (b) in subimages.

![](img/f73ae67732328dc36596b27ffe8d0152_510_0.png)

**FIGURE 9.42:** Multiresolution rendering of 93 slices of 64 x 64, 8-bit image using iso-surfacing with the marching cubes algorithm.

![](img/f73ae67732328dc36596b27ffe8d0152_510_1.png)

**FIGURE 9.43:** Low resolution rendering except for the ROI (nose portion of the head).

![](img/f73ae67732328dc36596b27ffe8d0152_511_0.png)

**FIGURE 9.44:** Low resolution rendering except for the ROI (left side ear portion of the head).

![](img/f73ae67732328dc36596b27ffe8d0152_511_1.png)

### 9.11.4 Summary

The 3D wavelet decomposition and reconstruction algorithm is useful for 3D image visualization. It improves the speed of rendering algorithm and achieves data compression by using a region of interest approach.

## 9.12 GEOPHYSICAL APPLICATIONS

Geophysical applications include characterization of subsurface geological structure; location and identification of subsurface objects; and estimation, mapping, and monitoring of material properties. A comprehensive discussion is beyond the scope of this book. We will, instead, concentrate on a few applications related to oil and gas exploration and production.

The primary goal of oilfield exploration is to identify, quantify, produce, and monitor oil and gas (in general, hydrocarbons) reserves. Hydrocarbons reside in rocks that are porous in nature. Earth formation can be viewed as a layered medium with each layer having its own properties. Some of these properties are conductivity, permittivity, density, elasticity, porosity,† and permeability.‡

Two main data acquisition techniques are seismic and well logging. A seismic source generates acoustic or elastic waves that propagate through the earth formation. Reflections from various layers are recorded in receivers (geophones for land seismic or hydrophones for marine). The amount of data to be processed is huge. Seismic images are basically maps of acoustic impedance. These images can provide valuable information on oilfield reserve. Well logging, on the other hand, gives higher spatial resolution data. In a typical exploration environment, a wellbore (15 to 30 cm in diameter) is drilled to a depth that may extend to a few kilometers. Formation properties are measured using a combination of sensors (electromagnetic, nuclear, acoustic, optical, etc.) that move along the wellbore trajectory. Material properties as a function of depth are known as a “log.”

Wavelet analysis has been used extensively in seismic data analysis, fluid identification, well log data processing and interpretation, upscaling, denoising, detection of abnormalities, processing of nonstationary pressure transient signals, long-term downhole signals, and many others [25–50]. In fact, it was the work of Morlet et al. [25, 26] in the 1980s on problems related to seismic signal that revived the interest in wavelets. A few applications of wavelets are briefly described in the next sections.

### 9.12.1 Boundary Value Problems and Inversion

Most applications of wavelets are in geophysical data analysis and interpretation. There are, however, some limited work in applying wavelets to boundary value problems and inversions in geophysics. Moridis et al. [27], for instance, have applied wavelets to solve the Buckley-Leverett nonlinear partial differential equation (PDE) arising from two-phase flow in one dimension. The equation can be represented as

```
R(x, t) = \frac{\partial S}{\partial t} + u \frac{\partial f(S)}{\partial x} = 0,
(9.50)
```

where \( S \) is the water saturation, \( (x, t) \) are space and time variables respectively, \( u \) is a parameter relating the porosity, the cross-section and the injection rate. The term \( f(S) \) is a nonlinear function that depends on the mobilities of oil and water and the corresponding irreducible saturations.

Two classes of wavelet bases (Daubechies and Chui-Wang) and two methods (Galerkin and collocation) are reported in the paper by Moridis et al. [27]. (See Chapter 10 for details on wavelets in boundary value problems.) The paper concludes that the Chui-Wang wavelets and a collocation method provide the optimum wavelet solution for the problem.

For many inverse problems, accounting for model uncertainty is an important issue, and Bayesian model averaging is commonly used for such purposes. This, however, requires choosing many model parameterizations and computing the posterior distribution for each model from scratch. For a 1D seismic problem and generally for linear inverse problems, Bennett and Malinverno [38] show how wavelets provide a multiresolution family of model parameterizations and further give a fast algorithm for converting the posterior distribution for one model to another when changing its local resolution. Gholami and Siahkoohi [50] have applied wavelets to solve linear and nonlinear inverse problems by constraining the solution to have sparse representations in two appropriate transformation domains simultaneously. They verified the effectiveness of the method by applying it to synthetic examples as well as field data from seismic travel time. Lu and Horne [33] have also applied wavelets and inverse
