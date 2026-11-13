![](bbox=[0.232, 0.123, 0.923, 0.296])

Figure 6.3. Vorticity of a 2D fluid flow. Note the alternation between vortices with opposite spinning directions. (Image courtesy of I. Barosan, Eindhoven University, the Netherlands.)

To compute divergence and vorticity and related quantities, we need the partial derivatives of the vector field components. On a discrete dataset, these can be approximated using the formulas specific for every grid cell type given in Section 3.7. However, as with all discrete datasets, derivatives can be sensitive to noise, so the results of such computations must be interpreted carefully.

# 6.2 Vector Glyphs

Vector glyphs are probably the simplest, and fastest, and most popular technique for visualizing vector fields. The vector glyph mapping technique essentially associates a vector glyph, or *vector icon*, with every sample point of the vector dataset. Various properties of the icon, such as location, direction, orientation, size, and color, are adjusted to reflect the value of the vector attribute it represents. The name *glyph*, meaning “sign” in Greek, reflects this principle of associating discrete visual signs with individual vector attributes. Every glyph is a sign that conveys, by its appearance, properties of the represented vector, such as direction, orientation, and magnitude.

Line glyphs. There are many variations of this framework for vector glyphs. Essentially, they propose various trade-offs between sampling density (how many glyphs we can display on a given screen area) and number of encoded attributes (how many attributes we can display per glyph). We shall present a number of vector glyphs, starting with the simplest one: the line. Lines essentially show the position, direction, and magnitude of a set of vectors. Given a vector dataset