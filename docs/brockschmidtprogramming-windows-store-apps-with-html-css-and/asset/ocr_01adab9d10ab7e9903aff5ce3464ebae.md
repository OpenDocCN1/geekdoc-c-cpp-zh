*In [this] box model, the children of a box are laid out either horizontally or vertically, and unused space can be assigned to a particular child or distributed among the children by assignment of 'flex' to the children that should expand. Nesting of these boxes (horizontal inside vertical, or vertical inside horizontal) can be used to build layouts in two dimensions.*

The specific display styles for Store apps are `display: -ms-flexbox` (block level) and `display: -ms-inline-flexbox` (inline). For a complete reference of the other supported properties, see the Flexible Box ("Flexbox") Layout documentation.<sup>76</sup>

| CSS Style | JavaScript Property (element.style.) | Values |
| --- | --- | --- |
| `-ms-flex-align` | `msFlexAlign` | `start` \| `end` \| `center` \| `baseline` \| `stretch` |
| `-ms-flex-direction` | `msFlexDirection` | `row` \| `column` \| `row-reverse` \| `column-reverse` \| `inherit` |
| `-ms-flex-flow` | `msFlexFlow` | `<direction> <wrap>` where `<direction>` is an `-ms-flex-direction` value and `<wrap>` is an `-ms-flex-pack` value |
| `-ms-flex-order` | `msFlexOrder` | `<integer>` (ordinal group) |
| `-ms-flex-pack` | `msFlexPack` | `start` \| `end` \| `center` \| `justify` |
| `-ms-flex-wrap` | `msFlexWrap` | `none` \| `wrap` \| `wrap-reverse` |

As with all styles, Blend is a great tool in which to experiment with different flexbox styles because you can see the effect immediately. It's also helpful to know that flexbox is used in a number of places around WinJS and in the project templates, as we saw with the Fixed Layout template earlier. The ListView control in particular takes advantage of it, allowing more items to appear when there's more space. The FlipView uses flexbox to center its items, and the Ratings, DatePicker, and TimePicker controls all arrange their inner elements using an inline flexbox. It's likely that your own custom controls will do the same.

# ## Nested and Inline Grids

Just as the flexbox has both block level and inline models, there is also an inline grid: `display: -ms-inline-grid`. Unlike the block level grid, the inline variant allows you to place several grids on the same line. This is shown in the InlineGrid example for this chapter, where we have three `div` elements in the HTML that can be toggled between inline (the default) and block level models:

```
    //Within the activated handler
    document.getElementById("chkInline").addEventListener("click", function () {
        setGridStyle(document.getElementById("chkInline").checked);
    });
```

<sup>76</sup> If you're accustomed to the `-ms-box` styles for flexbox, Microsoft aligned to the W3C specifications as they existed at that time for Windows 8 and Internet Explorer 10. As of Windows 8.1 and Internet Explorer 11, the `[-ms-]` prefixes are apparently no longer needed, but as of this writing they are still what's recognized by Visual Studio's IntelliSense, so I'm showing them as such here.