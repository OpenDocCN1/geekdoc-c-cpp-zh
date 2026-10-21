# Storing and Printing Documents

The first step is to output the file name that you squirrelled away in the `CPrintInfo` object. The `SetTextAlign()` function member of the CDC object allows you to define the alignment of subsequent text output in relation to the reference point you supply for the text string in the `TextOut()` function. The alignment is determined by the constant passed as an argument to the function. You have three possibilities for specifying the alignment of the text:

| Constant | Alignment |
|---|---|
| `TA_LEFT` | The point is at the left of the bounding rectangle for the text, so the text is to the right of the point specified. This is default alignment. |
| `TA_RIGHT` | The point is at the right of the bounding rectangle for the text, so the text is to the left of the point specified. |
| `TA_CENTER` | The point is at the center of the bounding rectangle for the text. |

You define the *x* coordinate of the file name on the page as half the page width, and the *y* coordinate as 20 units, which is 0.2 inches, from the top of the page. After outputting the name of the document file as centered text, you reset the text alignment to the default, `TA_LEFT`, for the text in the document.

The `SetTextAlign()` function also allows you to change the position of the text vertically by ORing a second flag with the justification flag. The second flag can be any of the following:

| Constant | Alignment |
|---|---|
| `TA_TOP` | Aligns the top of the rectangle bounding the text with the point defining the position of the text. This is the default. |
| `TA_BOTTOM` | Aligns the bottom of the rectangle bounding the text with the point defining the position of the text. |
| `TA_BASELINE` | Aligns the baseline of the font used for the text with the point defining the position of the text. |

The next action in `OnPrint()` uses the method that I discussed for mapping an area of the document to the current page. You get the document drawn on the page by calling the `OnDraw()` function that is used to display the document in the view. This potentially draws the entire document, but you can restrict what appears on the page by defining a **clip rectangle**. A clip rectangle encloses a rectangular area in the device context within which output appears. Output is suppressed outside of the clip rectangle. It’s also possible to define irregularly shaped areas for clipping called **regions**.

The initial default clipping area defined in the print device context is the page boundary. You define a clip rectangle which corresponds to the 600 by 900 area centered in the page. This ensures that you draw only in this area, and the file name is not to be overwritten.

After the current page has been drawn, you call `SetClipRgn()` with a `NULL` argument to remove the clip rectangle. If you don’t do this, output of the document title is suppressed on all pages after the first because it lies outside the clip rectangle that would otherwise remain in effect in the print process until the next time `IntersectClipRect()` gets called.