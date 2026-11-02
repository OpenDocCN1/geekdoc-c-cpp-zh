
the appearance of controls. In fact, absolutely everything that's visually different between HTML controls in a Windows Store app and the same controls on a web page is due to styling and styling alone.

**Design help** Some higher-level design guidance for styling is available in the documentation: Branding your Windows Store apps.

For both HTML and WinJS controls, CSS standards apply including pseudo-selectors like `:hover`, `:active`, `:checked`, and so forth, along with `-ms-*` prefixed styles for emerging standards.

For HTML controls, there are also additional `-ms-*` styles—that aren't part of CSS3—to isolate specific parts of those controls. This is because the constituent parts of such controls don't exist separately in the DOM. So pseudo-selectors—like `::ms-check` to isolate a checkbox mark and `::ms-fill-lower` to isolate the left or bottom part of a slider—allow you to communicate styling to the depths of the rendering engine. In contrast, all parts of WinJS controls are addressable in the DOM, so they are just styled with specific `win-*` classes defined in the WinJS stylesheets and the controls are simply rendered with those style classes. Default styles are defined in the WinJS stylesheets, but apps can override any aspect of those to style the controls however you want.

In a few cases, as already pointed out, certain `win-*` classes define style packages for use with HTML controls, such as `win-backbutton`, `win-vertical` (for a slider) and `win-ring` (for a progress control). These are intended to style standard HTML controls to look like special system controls.

There are also a few general purpose `-ms-*` styles (not selectors) that can be applied to many controls (and elements in general), along with some general WinJS `win-*` style classes. These are summarized in the following table.

| Style or Class | Description |
|---|---|
| `-ms-user-select: none \| inherit \| element \| text \| auto` | Enables or disables selection for an element. Setting to `none` is particularly useful to prevent selection in text elements. |
| `-ms-zoom: <percentages>` | Optical zoom (magnification). |
| `-ms-touch-action: auto \| none (and more)` | Allows specific tailoring of a control's touch experience, enabling more advanced interaction models. |
| `-ms-touch-select: grippers \| none` | Toggles "gripper" visual elements for touch text selection. |
| `win-interactive` | Prevents default behaviors for controls contained inside ItemContainer, FlipView, and ListView controls (see Chapter 7 for the latter two). |
| `win-swipeable` | Sets `-ms-touch-action` styles so a control within a ListView can be swiped (to select) in one direction without causing panning in the other. |
| `win-small, win-medium, win-large` | Size variations to some controls. |
| `win-textarea` | Sets typical text editing styles. |

For all of these and more, spend some time with these three reference topics: WinJS CSS classes for typography, WinJS CSS classes for HTML controls, and CSS classes for WinJS controls. I also wanted to provide you with a summary of all the other vendor-prefixed styles (or selectors) that are supported within the CSS engine for Store apps; see the next table. Vendor-prefixed styles for animations, transforms, and transitions are still supported, though no longer necessary, because these standards have recently been finalized. I made this list because the documentation here can be hard to penetrate: you have to click through the individual pages under the Cascading Style Sheets topic in the docs to see what little bits have been added to the CSS you already know.

| Area | Styles |
|---|---|
| Backgrounds and borders | -ms-background-position-[x \| y] |
| Box model | -ms-overflow-[x \| y] |
| Basic UI | -ms-text-overflow (for ellipses rendering)<br>-ms-user-select (sets or retrieves where users are able to select text within an element)<br>-ms-zoom (optical zoom) |
| Exclusions | -ms-wrap-flow [margin \| through] |
| Grid | -ms-grid and -ms-grid-column [column-align \| columns \| column-span \| grid-layer \| row \| row-align \| rows \| row-span] |
| High contrast | -ms-high-contrast-adjust |
| Regions | -ms-flow-from [into] along with the MSRangeCollection method |
| Text | -ms-block-progression, -ms-hyphens and -ms-hyphenate-limit-chars [chars \| lines \| zone], -ms-text-align-last, -ms-word-break, -ms-word-wrap, -ms-line-mode, -ms-layout-grid and -ms-layout-grid-char [char \| line \| mode \| type], and -ms-text-autospace [justify \| ideograph \| under-line-position] |
| Panning and Zooming | -ms-content-zoom [chaining \| limit \| limit-max \| limit-min \| snap \| snap-points \| snap-type], -ms-content-zooming, -ms-overflow-style, -ms-scroll-[chaining \| limit-max \| limit-min \| limit-x \| limit-y \| max \| min \| rail \| rails \| snap-points-x \| snap-points-y \| snap-type \| snap-x \| snap-y \| translation] |
| Other | -ms-writing-mode |

## Styling Gallery: HTML Controls

Now we get to enjoy a visual tour of styling capabilities for Windows Store apps. Much can be done with standard styles, and then there are all the things you can do with special styles and pseudo-elements as shown in the graphics in this section. The specifics of all these examples can be seen in the HTML essential controls sample.

Also check out the very cool Applying app theme color (theme roller) sample. This beauty lets you configure the primary and secondary colors for an app, shows how those colors affect different controls, and produces about 200 lines of precise CSS that you can copy into your own stylesheet; you can also copy the appropriate color code into the branding fields of your manifest and use them in other branding graphics. This very much helps you create a color theme for your app, which we very much encourage to establish an app's own personality within the overall Windows design guidelines and not try to look like the system itself. (Do note that controls in system-provided UI, like the confirmation flyout when creating secondary tiles, system toast notifications, and message dialogs, will be styled with system colors. These cannot be controlled or duplicated by the app.)

### Button (background-color)

### Progress (color)

### Select (background-color, color, border, font)

### Text Area (transform)

### Checkbox/Radiobutton (background-image and :checked)

### Checkbox/Radiobutton

```
CSS pseudo-element: input[type="checkbox"].class::ms-check {color}
```

```
CSS pseudo-element: input[type="checkbox"].class::ms-check {image}
```

```
CSS pseudo-element: input[type="radio"].class::ms-check {color}
```

### File upload

```
CSS pseudo-element: input[type="file"].class::ms-value
```

```
CSS pseudo-element: input[type="file"].class::ms-browse
```

### Text Input (most forms)

```
CSS pseudo-element: input[type="text"].class::ms-value
```

```
CSS pseudo-element: input[type="text"].class::ms-input-placeholder
```

```
CSS background image (and other styles)
```

```
CSS pseudo-element: input[type="text"].class::ms-clear
```

### Progress

```
CSS pseudo-element:
progress.class::ms-fill {
  -ms-animation-name: ms-ring;
}
```

```
CSS pseudo-element: progress.class::ms-fill (background-image, etc)
```

### Text Input (password)

```
CSS pseudo-element: input[type="password"].class::ms-reveal
```

- Fruits
  - Apple
  - Banana
  - Grape
- Vegetables
  - Broccoli
  - Carrot
  - Eggplant

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_254_0.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_254_1.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_254_2.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_254_3.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_254_4.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_254_5.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_254_6.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_254_7.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_254_8.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_254_9.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_255_0.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_255_1.png)

**Note** Though not shown here, you can also use the `-ms-scrollbar-*` styles for scrollbars that appear on pannable content in your app.

## Styling Gallery: WinJS Controls

Similarly, here is a visual rundown of styling for WinJS controls, drawing again from the samples in the SDK: HTML DatePicker and TimePicker controls, HTML Rating control, HTML ToggleSwitch control, HTML Tooltip control, a modified version of the HTML Item Container sample (in the companion content), and the Navigation and navigation history sample. The latter specifically shows a little styling of the BackButton control. Scenario 4 (`css4/BackButton.css`) overrides a few styles in the `win-navigation-backbutton` class to change the control's size. More generally, the back button control
