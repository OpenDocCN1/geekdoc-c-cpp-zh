| Table 12.2: Properties of the Graphics Class |
| Property | Description |
| RenderingOrigin | Gets or sets the rendering origin of the Graphics object for dithering and hatch brushes. |
| SmoothingMode | Gets or sets the rendering quality for the Graphics object. |
| TextContrast | Gets or sets the gamma correction value for rendering text. The gamma correction value is used for rendering the ClearType text. It must be between 0 and 12 and the default value is 4. |
| TextRenderingHint | Gets or sets the rendering mode for the text associated with the Graphics object. |
| Transform | Gets or sets a copy of the transformation for the Graphics object. |
| VisibleClipBounds | Retrieves the bounding rectangle for the area of clipping region of the Graphics object. |

The noteworthy methods of the Graphics class are listed in Table 12.3:

| Table 12.3: Methods of the Graphics Class |
| Method | Description |
| BeginContainer | Saves a graphics container with the current state of the Graphics object and opens and uses a new graphics container |
| Clear | Clears the entire drawing surface and fills it with the specified background color |
| CopyFromScreen | Performs a bit-block transfer of color data from the screen to the drawing surface of the Graphics object |
| Dispose | Releases all the resources used by the Graphics object |
| DrawArc | Draws an arc representing a portion of ellipse |
| DrawBezier | Draws a Bezier curve defined by four point structure |
| DrawBeziers | Draws a series of Bezier curves |
| DrawClosedCurve | Draws a closed cardinal curve |
| DrawCurve | Draws a cardinal curve |
| DrawEllipse | Draws an ellipse defined by a bounding rectangle |
| DrawIcon | Draws an image represented by the specified icon |
| DrawIconUnstretched | Draws an image without scaling the image |
| DrawImageUnscaled | Draws an image using its original physical size at the location specified |
| DrawImageUnscaledAndClipped | Draws the specified image without scaling and clips to fit the rectangle |
| DrawLine | Draws a line connecting the two points specified by the coordinate pairs |
| DrawLines | Draws a series of line segments that connect an array of points |
| DrawPath | Draws a series of connected lines and curves |
| DrawPie | Draws a pie shape defined by an ellipse |
| DrawPolygon | Draws a polygon defined by an array of the Point structure |
| DrawRectangle | Draws a rectangle specified by a coordinate pair, a width, and a height |
| DrawRectangles | Draws a series of rectangles defined by the Rectangle structure |
| DrawString | Draws a text string at the specified location with the Brush and Font objects |
| EndContainer | Closes the current graphics container and restores the state of the Graphics object |
| Equals | Determines whether the specified object is equal to the current object |