# Barycentric Mappings*

Teseo Schneider

Università della Svizzera italiana, Lugano, Switzerland

# CONTENTS

+   4.1 Introduction .................................... 64
+   4.1.1 Convex polygons ............................... 64
+   4.1.2 Arbitrary polygons ............................ 65
+   4.2 Bijective barycentric mapping ................... 66
+   4.2.1 Perturbed target polygons ..................... 66
+   4.3 Bijective composite barycentric mapping ......... 68
+   4.3.1 Limit of composite barycentric mappings ....... 70
+   4.4 Extensions ...................................... 71
+   4.4.1 Closed planar curves .......................... 71
+   4.4.2 Polyhedra ..................................... 73
+   4.5 Practical considerations ........................ 75
+   4.5.1 Choosing the coordinates ...................... 75
+   4.5.2 Choosing the vertex paths ..................... 75

BARYCENTRIC MAPPINGS allow us to naturally warp a source polygon to a corresponding target polygon, or, more generally, to create mappings between closed curves or polyhedra. Unfortunately, bijectivity of such barycentric mappings can only be guaranteed for the special case of warping between convex polygons. In fact, for any barycentric coordinates, it is always possible to construct a pair of polygons such that the barycentric mapping is not bijective. However, if the two polygons are sufficiently close, the mapping is close to the identity and hence bijective. This fact suggests "splitting" it into several intermediate mappings and creating a composite barycentric mapping, which is guaranteed to be bijective between arbitrary polygons, polyhedra, or closed planar curves.