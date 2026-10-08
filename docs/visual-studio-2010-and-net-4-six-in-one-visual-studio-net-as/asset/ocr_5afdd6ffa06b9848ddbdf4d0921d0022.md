the data source to the UI element, the convert back function is called when the UI element's property value is loaded back to the data source. Both functions receive two parameters — the value that is to be converted, and a Sys.Binding instance that you can use to query any information about the source and the target of the binding. Although this feature also works with global functions, it is recommended that you implement the convert methods as members of the Sys.converters object.

The following markup renders a textbox and a disabled button. The goal is to enable the button only if the user enters " Accept."

If you accept the agreement please type "I Accept" here:

```
<input type="text"
sys:value={ binding binding,
source={{ btn }}},
mode=OneWayToSource,
convertBack=disabledConverter,
expectedResult=I Accept />

<br />
<input type="button"
id="btn"
value="Submit registration " />
```

Code file [3-AjaxLibrary\14-Converters.htm] available for download at Wrox.com

As you can see from the syntax, button's disabled property (source) is bound to the value of the textbox (target). By default the binding would be two-way, but the behavior is changed to OneWayToSource because you would not want to display the disabled property (true or false) in the textbox. You, ensure that the data flows from the textbox to the button.

However, there is still a type mismatch between the string value and the Boolean disabled properties. To overcome this, a custom function called disabledConverter is created. It is configured as a convertBack method so the template engine will call it when the value of the target (textbox) is transferred to the source (button) — and that is exactly what is needed. The disabledConverter function is implemented with nothing special about this situation, so you can easily reuse it anywhere else in your code.

```
Sys.converters.disabledConverter = function(value, binding)
{
    return (value != binding.expectedResult);
}
```

Code file [3-AjaxLibrary\14-Converters.htm] available for download at Wrox.com

Figure 19-11 shows the result page.

One thing to note is that the "I Accept" value is not hard-coded into the converter, but rather it is passed as a parameter. You can add additional parameters to your binding syntax, and all of them will be added as expanding properties

![](bbox=[0.605, 0.853, 0.88, 0.903])

FIGURE 19-11: The button is disabled with live binding