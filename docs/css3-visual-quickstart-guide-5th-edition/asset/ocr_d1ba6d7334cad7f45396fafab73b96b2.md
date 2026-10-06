# 2. Specify the vertical alignment.

super;
type a value for a vertical text alignment using one of these options:

+   - super superscripts the text above the baseline.

+   - sub subscripts the text below the baseline.

+   - baseline places the text on the baseline (its default).

+   - A relative value from Table 6.8 that sets the element's alignment relative to its parent's. To align the top of your text with the top of the parent element's text, for example, you would use **text-top**.

+   - A percentage value, which raises or lowers the element's baseline proportionate to the parent element's font size (25%, for example).

# TABLE 6.8 Setting an Element's Position Relative to the Parent Element

| Type | To align the element |
| --- | --- |
| top | Top to highest element in line |
| middle | Middle to middle of parent |
| bottom | Bottom to lowest element in line |
| text-top | Top to parent element's text |
| text-bottom | Bottom to bottom of parent element's text |

# Math and Science

Supcript and subscript are used for scientific notation. To express the Pythagorean theorem, for example, you would use superscripts:

```
a² + b² = c²
```

A water molecule might be expressed with subscripts as:

H₂O

However, keep in mind that neither subscript nor superscript will reduce the text size, so you may also want to include **font-size** in your definition to achieve a true scientific notation style. (See "Setting the Font Size" in Chapter 5).

> TIP Superscript is great for footnotes, which can be hyperlinked to notes at the bottom of the current page or to another Web Page.

> TIP The sup and sub tags can also be used as superscript and subscript, but should not be used for design (as in this case) for footnotes or mathematical notation.

> TIP If you are creating a multicolumn layout, you might encounter problems with vertical alignment when it doesn't appear where it should be. In those cases, a good fallback is to use relative positioning, as explained in Chapter 10.