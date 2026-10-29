# Setting Painter Options

At the bottom of the Paint Deformation rollout is a button labeled Brush Options. Clicking this button opens the Painter Options dialog box, shown in Figure 26.5. Using this dialog box, you can set several customized brush options, including the sensitivity of the brush.

# Cross-Ref

The Painter Options dialog box is also used by the brushes to paint vertex colors for the Vertex Paint modifier and to paint skin weights as part of the Skin modifier. The Vertex Paint modifier is covered in Chapter 33, “Creating Baked Textures and Normal Maps,” and the Skin modifier is covered in Chapter 40, “Skinning Characters.”

# FIGURE 26.5

The Painter Options dialog box includes a graph for defining the minimum and maximum brush strengths and sizes.

![](bbox=[0.07, 0.58, 0.55, 0.82])

The Min/Max Strength and Min/Max Size values determine the minimum and maximum weight values and paint gizmo sizes. You can define the brush falloff using the curve. This keeps the weights from making an abrupt change (muscles tend to look funny when this happens). Under the curve are several buttons for quickly defining the shape of the falloff curve, including Linear, Smooth, Slow, Fast, and Flat.

The Display Options section includes options that determine the look of the painting gizmo. The Draw Ring, Draw Normal, and Draw Trace options make a ring; the surface normal or an arrow showing the trace direction appears. The Normal can be scaled, and the Marker option displays a small circular marker at the end of the normal.

The Pressure Options let you paint using a graphics tablet with the pressure applied to affect the Strength, Size, or a combination. You can enable Pressure Sensitivity for the brush gizmo. The options include None, Strength, Size, and Both. Using the graph, you can predefine Strength and Size pressure curves and then select to use them.

The Mirror option paints symmetrically on the opposite side of the gizmo across the specified axis. You can also set an Offset and the Gizmo Size. This is handy for muscles that you want to deform symmetrically.

In the Miscellaneous section, the Tree Depth, Update on Mouse Up, and Lag Rate options control how often the scene and the painted strokes are updated.