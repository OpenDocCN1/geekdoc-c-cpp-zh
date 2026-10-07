# AUGMENTED ARROWS

The ScrollBar's arrows are actually RepeatButtons. If you click on one, the control's value changes by the SmallChange value. If you hold an arrow down, the value changes by that amount repeatedly.

# SLIDER

Like the ScrollBar control, the Slider controls the user select a numeric value from a range of values. The Slider works in almost exactly the same way as the ScrollBar but with a different appearance.

**Figure 7-16** shows the UseSlider example program. How similar this program is to the UseScrollBar program shown in Figure 7-15. The main differences are that the Sliders display ticks and do not have arrows.

![](bbox=[0.558, 0.517, 0.931, 0.597])

FIGURE 7-16

The Slider has many of the same properties as the ScrollBar. See the table in the previous section for a description of the most important of those properties.

The following table summarizes new properties that the Slider uses to define its tick marks:

| PROPERTY | PURPOSE |
| --- | --- |
| IsSnapToTick | If this is True, then the control snaps its value to the nearest tick mark. |
| IsSelectionRangeEnabled | Determines whether the user can select a range of values rather than only a single value. |
| TickFrequency | Determines the numeric spacing between tick marks. |
| TickPlacement | Determines the position of the tick marks. This can be Both (both top and bottom if horizontal or left and right if vertical), BottomRight (bottom if horizontal or right if vertical), TopLeft (top if horizontal or left if vertical), or None. |