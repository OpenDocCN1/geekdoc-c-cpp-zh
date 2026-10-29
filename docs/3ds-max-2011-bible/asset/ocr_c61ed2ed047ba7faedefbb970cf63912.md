# Part III: Modeling Basics

# FIGURE 14.16

All the Edge specific commands are available when the Edge subobject mode is enabled. Many of the Border subobject commands are the same as those for Edges.

![](bbox=[0.075, 0.184, 0.483, 0.315])

# Insert Vertices

You also can access the caddy for the Bridge feature. This caddy offers the options to Bridge Specific Edges or to Use Edge Selection. The Bridge Specific Edges option has two buttons for each edge. If you click one of these buttons, you can select an edge in the viewport. The Use Edge Selection option lets you drag a marquee in the viewport to select the edges. The Bridge Edges caddy also includes options for the number of Segments, the Smooth value, and a Bridge Adjacent value, which increases the triangulation for angles above the given threshold.

# Split and Insert Vertex

The Split button adds a new vertex at the middle of the edge and splits the edge into two equal sections. This button is handy when you need to increase the resolution of a section quickly.

The Insert Vertex button lets you add a new vertex anywhere along an edge. The cursor changes to crosshairs when it is over an edge. Click to create a vertex. When in Edge, Border, Polygon, or Element subobject mode, this button also makes vertices visible. Within the Ribbon's Edges page, you can set the number of vertices to be placed evenly along the selected edges using the number spinner next to the Insert Vertices tool.

# Create Shape from Selection

The Create Shape from Selection button creates a new spline shape from selected edges. You can also select options for Smooth or Linear shape types.

# Spin

The Spin button rotates the hidden edges that break up the polygon into triangles (all polygonal faces include these hidden edges). For example, if a quadrilateral (four-sided) face has a hidden edge that runs between vertices 1 and 3, then the Spin button changes this hidden edge to run between vertices 2 and 4. This affects how the surface is smoothed when the polygon is not coplanar.

# Cap Poly

The Cap Poly button that appears in the Geometry (All) panel causes the existing border selection to be filled in with a single coplanar polygon. After using this feature, the Border subobject is no longer identified as a Border subobject.

# Bridge

The Bridge feature joins two selected Border subobjects with a tube of polygons that connect the two borders. The two selected borders must be part of the same object and need not have an equal number of segments.