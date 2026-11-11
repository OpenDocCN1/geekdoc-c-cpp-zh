+   **java.awt.Graphics2D** 1.2
+   
+   - `void clip(Shape s)`
+     intersects the current clipping shape with the shape s.
+   - `FontRenderContext getFontRenderContext()`
+     returns a font render context that is necessary for constructing TextLayout objects.

+   **java.awt.font.TextLayout** 1.2
+   
+   - `TextLayout(String s, Font f, FontRenderContext context)`
+     constructs a text layout object from a given string and font, using the font render context to obtain font properties for a particular device.
+   - `float getAdvance()`
+     returns the width of this text layout.
+   - `float getAscent()` / `float getDescent()`
+     returns the height of this text layout above and below the baseline.
+   - `float getLeading()`
+     returns the distance between successive lines in the font used by this text layout.

# ### 11.3.8 Transparency and Composition

In the standard RGB color model, every color is described by its red, green, and blue components. However, it is also convenient to describe areas of an image that are *transparent* or *partially transparent*. When you superimpose an image onto an existing drawing, the transparent pixels do not obscure the pixels under them at all, whereas partially transparent pixels are mixed with the pixels under them. Figure 11.51 shows the effect of overlaying a partially transparent rectangle on an image. You can still see the details of the image shine through from under the rectangle.

In the Java 2D API, transparency is described by an *alpha channel*. Each pixel has, in addition to its red, green, and blue color components, an alpha value between 0 (fully transparent) and 1 (fully opaque). For example, the rectangle in Figure 11.51 was filled with a pale yellow color with 50% transparency:

```
```
new Color(0.7f, 0.7f, 0.0f, 0.5f);
```
```