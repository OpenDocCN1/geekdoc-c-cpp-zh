# CHAPTER 4 COMMON PROPERTIES

+   - FontSize Determines the size of the font in pixels. This gives the size of the characters and doesn't include leading and internal space that may be drawn above and below a line of text. You can add the unit specifiers 'px' or 'pt' to indicate pixels or printer's points (1/7 inch). For example, the value '20pt' means that the text should be 20 points.

+   - TextStyle Determines the text's style. This property can take the values Normal and Italic.

+   - FontWeight Determines the text's density (whether it is bold or not). This property can take the values (in increasing order of density) Thin, ExtraLight, Light, Normal, Medium, SemiBold, Bold, ExtraBold, and ExtraBlack. The FontProperties program shown in Figure 4-5 demonstrates an assortment of property values. Notice how much taller the 20-point font is compared to the 21-pixels New Roman.

For a particular colum, some FontWeight values may produce the same results. For example, on my computer the Arial font (and most), the values Thin through Medium produce a normal font and SemiBold through ExtraBold produce the same font bold. In contrast, my computer displays the Arial font's ExtraBold through ExtraBlack values with a slightly darker band than the Bold value.

The Weights example program shown in Figure 4-6 displays text in 20-pixel Arial and fonts at different weights. You can tell that Arial gives three different weights by looking closely at the widths of the text Arial in the column on.

# COLOR

Several properties determine a control's appearance. For drawing controls such as Ellipse, Rectangle, and Path, the stroke property property determines the brush used to draw the shape's outline, and the Fill property determines how the shape is filled.

For non-drawing controls such as Label, TextBox, and StackPanel, the Background property determines how the control's interior is filled, and the Foreground property determines how objects displayed on top of the control appear.

![](bbox=[0.565, 0.213, 0.875, 0.363])

FIGURE 4-5

![](bbox=[0.565, 0.498, 0.875, 0.748])

FIGURE 4-6

# A NEEDLESS INCONSISTENCY

Yes, it might have been nice if these objects used either Foreground/Background or Stroke/Fill—but that is not the way WPF works.