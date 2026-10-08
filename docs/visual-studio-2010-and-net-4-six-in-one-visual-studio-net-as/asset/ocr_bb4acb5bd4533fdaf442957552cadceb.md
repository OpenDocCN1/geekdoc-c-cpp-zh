# TABLE 14-9 (continued)

| ANNOTATION TYPE | DESCRIPTION |
| --- | --- |
| LineAnnotation | This represents a line annotation. You can use the StartCap and EndCap properties to set the cap styles for the line's ends. |
| HorizontalLineAnnotation | This represents a horizontal line annotation, and derives from LineAnnotation. |
| VerticalLineAnnotation | This represents a vertical line annotation, and derives from LineAnnotation. |
| TextAnnotation | This represents a text annotation. You can use the Text property to define the text you want to show in the annotation. You can use data point values such as #VALX, #VAL, #TOTAL, and so. (Listing 14-10 and the related comments them.) The Multiline property can get or set the flag indicating whether the annotation text is multi-line. |
| RectangleAnnotation | This represents a rectangle with text annotation, and derives from TextAnnotation. It allows you to enclose the text in a rectangle, and provides about a dozen properties to customize the rectangle border and fill |
| EllipseAnnotation | This represents an ellipse with text annotation, and derives from TextAnnotation. It allows you to enclose the text in an ellipse, and provides about dozen properties to customize the ellipse border and fill. |
| ArrowAnnotation | This represents an arrow annotation. Arrow annotations can be used to connect points on the chart, or to highlight a single chart area. You can define the style and size of arrow with the ArrowStyle and ArrowSize properties, respectively. |
| Border3DAnnotation | This represents an annotation with a three-dimensional border, and derives from RectangleAnnotation. Use the BorderSkin compound property to set the attributes of the border. |
| CalloutAnnotation | This represents a callout with text annotation, and derives from TextAnnotation. You can set the style of the callout line anchor cap and the annotation callout style with the CalloutAnchorCap and CalloutStyle properties, respectively. |
| PolylineAnnotation | This represents a polyline annotation. You use the StartCap and EndCap properties to set the cap styles for the polyline's ends. There are two properties to set the path points of a polyline annotation. GraphicsPath can be used only at run-time, and GraphicsPathPoints is available only at design-time. |