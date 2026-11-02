The win-container, win-itembox, and win-item classes identify successive layers of the control as it's built up by its constructor. That is, in your markup you'll have one root element for the ItemContainer control that contains the item contents. When that control is instantiated, the win-container class is added to that root element and two more div elements with win-itembox and win-item are inserted before the item contents. The classes let you target each layer for styling. Note that the layers shown below all overlap one another; the offset is added only for visualization purposes:

```
<!-- Markup in your HTML file -->
<div class="[your classes]" data-win-control="WinJS.UI.ItemContainer">
  [your item content]
</div>
```

```
<!-- Results in the DOM -->
<div class="[your classes]">
  <div class="win-itembox">
    <div class="win-item">
      [your item content]
    </div>
  </div>
</div>
```

![](bbox=[0.2, 0.44, 0.6, 0.66])

In addition, a few more classes identify on the root element different control states or options:

| Style Class | State |
|---|---|
| win-swipeable | Added to controls with swipeBehavior set to select. |
| win-vertical | Added to controls with the vertical orientation. |
| win-horizontal | Added to controls with the vertical orientation. |
| win-selected | Added to controls that are in a selected state. |

The following series of images are taken from the modified HTML ItemContainer sample found in this chapter's companion content. First are some of the outline styles you can use. (Default styles are on the left, and somewhat ridiculous custom styles are shown on the right side with the applicable CSS.)