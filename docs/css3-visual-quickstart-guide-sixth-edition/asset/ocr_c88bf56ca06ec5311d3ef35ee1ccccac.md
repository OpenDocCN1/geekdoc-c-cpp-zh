| Value | |
|---|---|
| normal | |
| pre | |
| nowrap | |

# # Controlling White Space

As you've learned, browsers traditionally collapsed multiple spaces into a single space unless a `<pre>` tag was used. CSS lets you allow or disallow that space collapsing, as well as designate whether text can break at a space (similar to the `<nobr>` tag) using the `white-space` property (Table 6.12).

An excellent example of this is the mouse tail poem from Chapter 3 of *Alice's Adventures in Wonderland*. This poem is shaped like a curve mouse tail **A**. If the `white-space` property value is assigned `pre` for the `poem` class, all those spaces collapse **B**. However, if it's assigned a value of `nowrap`, the spaces and line breaks are ignored, and the text stretches as far to the right on the page as necessary **C**.

![](bbox=[0.065, 0.235, 0.305, 0.615])

**A** The `pre` value keeps all spaces so the poem retains its distinctive mouse tail shape rather than collapsing.

![](bbox=[0.205, 0.625, 0.795, 0.745])

**B** Without the `pre` value, the spaces collapse along with the mouse tail.

![](bbox=[0.205, 0.795, 0.795, 0.885])

**C** With the `no-wrap` value, the poem stretches vertically across the window, forcing a horizontal scroll to accommodate its width.