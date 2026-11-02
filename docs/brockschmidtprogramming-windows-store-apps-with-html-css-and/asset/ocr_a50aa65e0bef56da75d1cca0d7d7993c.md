![](bbox=[0.13, 0.08, 0.91, 0.34])

If you were to provide your own navigation buttons in the template (wired to the next and previous methods), hide the default by adding `display: none` to the `<control selector> .win-navbutton` style rule.

As we saw with the `ItemContainer` in Chapter 5, the FlipView creates some intermediate `div` elements between the root where you declare the FlipView and where the template gets rendered. These layers are classed with `win-flipview` (the root element), `win-surface` (the panning region), and `win-item` (where a template is rendered); you'll typically use these to style margins, padding, etc.:

```
```html
<!-- Markup in your HTML file -->
<div data-win-control="WinJS.Binding.Template">
  [your template content]
</div>

<div class="[your classes]" data-win-control="WinJS.UI.FlipView">
</div>
```
```

![](bbox=[0.14, 0.63, 0.75, 0.88])