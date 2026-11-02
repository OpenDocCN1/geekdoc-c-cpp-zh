![](bbox=[0.13, 0.12, 0.52, 0.33])

Next, click the drop-down next to the template property and select <Create New Template...>, which brings up the dialog below wherein you'll conveniently see the members of your data source. Check those you need and give your template a name:

![](bbox=[0.13, 0.45, 0.45, 0.72])

When you press OK, Blend will create unstyled markup in your HTML file and insert the appropriate reference in the control's options. Because I selected to identify the template with a class, the reference uses the select syntax:

```
<div class="seasonalItemTemplate" data-win-control="WinJS.Binding.Template">
  <div>
    <div data-win-bind="textContent:description"></div>
    <img data-win-bind="src:image" height="100" width="100">
    <div data-win-bind="textContent:subtitle"></div>
    <div data-win-bind="textContent:title"></div>
  </div>
</div>

<div data-win-control="WinJS.UI.Repeater" data-win-options="{data:Data.seasonalItems, template:select('.seasonalItemTemplate')}"></div>
```