If you combine all these tricks into a single page, you will get the result shown in Figure 19-5.

![](bbox=[0.14, 0.143, 0.859, 0.375])

FIGURE 19-5: Result of using pseudo columns in a template

# Running Code Inside a Template

It sometimes happens that the declarative syntax is not powerful enough to express the required functionality. In this case, you have no other than adding some code to the template. One of the most-required scenarios is to render or not render a specific element based on a return value of a JavaScript expression. The this is where `sys:if` attribute comes into the picture.

In one of the previous examples, you show how to display a value from the next record in the template by calling a custom function (`setNextCountry`). The this is where `sys:if` attribute, you can implement the same function without the external function:

```
<span sys:if='$index + 1 = $context.data.length">
nThe next country is {{ $context.data[$index + 1].Name}}.\</span>
```

> Code file 3-AjaxLibrary07-DataViewConditions.htm available for download at Wrox.com.

Here you can see how to use the `$index` and `$context` pseudo-columns to access the next record. The new part is the `sys:if` attribute that can contain arbitrary code that will be evaluated every time a item is rendered. If you add the `sys:if` attribute to an HTML element, that will be rendered only if the specified JavaScript expression evaluates to true. In this case, a span is rendered for every record except the last one.

Another common scenario is to render a tag for the first record, or before the first record. The following code snippet renders a drop-down list box with countries and a default "Select a country" before the first record:

```
<select
class="sys-template"
sys:attach="dv">
```