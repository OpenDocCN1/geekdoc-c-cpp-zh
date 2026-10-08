
Also, you can remove the first item from the collection by calling the removeAt method:

```
countries.removeAt(0);
```

Code file [3-AjaxLibraryII-LiveBinding.htm] available for download at Wrox.com

You can also call the original functions of the Sys.Observer class, but in this case, you must suspend the target object as well:

```
Sys.Observer.removeAt(countries,0);
```

Code file [3-AjaxLibraryII-LiveBinding.htm] available for download at Wrox.com

It is also possible to modify a property of the target object with the setValue method. However, if you modify properties and you do not want to risk the PropertyChanged event until all properties are updated (for example, to avoid UI flickering and partially updated records), you can suspend the notification, and then send it when you are done:

- countries.beginUpdate();
- Sys.Observer.setValue(countries[0], 'Name', 'Österreich');
- Sys.Observer.setValue(countries[0], 'Capital', 'Wien');
- Sys.Observer.setValue(countries[5], 'Name', 'Suomi');
- Sys.Observer.setValue(countries[7], 'Name', 'Magyarország');
- countries.endUpdate();

Code file [3-AjaxLibraryII-LiveBinding.htm] available for download at Wrox.com

The DataView is smart enough to recognize if a data source is observable, and is capable of handling the collection or property changed event automatically. Still, you must modify your data-binding syntax to identify which parts of the template should be updated when data changes:

```
<ul>
<li class="sys-template"
  sys:attach="dv"
  data:data="{ countries }">
  <li>
    <span>{ binding Name }</span
    <span>{ binding Capital }</span
  </li>
</ul>
```

Code file [3-AjaxLibraryII-LiveBinding.htm] available for download at Wrox.com

As you can see in this example, you use the binding markup extension, and then the name of the property you want to display. These placeholders will be automatically updated when the source data changes. However, note that you must always modify your data source via the Sys.Observer methods. If you modify the data source directly, without going through the interface, notification events will not be raised.

## Top-Level Binding

The live-binding syntax supports not only specifying the name of the property you want to bind, but also optional parameters. One of the additional parameters is the `source` that points to the object that property should be bound to the target control. Using the `source` parameter allows you to create top-level bindings, which means you can define data-binding expressions outside of a DataView.

You can create a global object, and you bind any of its properties to a `span`. What's more, if you make your global observable and use the live binding syntax, updates are immediately displayed on the UI:

```
<head>
<script type="javascript">
var country = ( Name: 'Magyarország', Code: 'hu', Capital: 'Budapest' );
Sys.Observer.make(country);

function translate() {
  Sys.Observer.setValue(country, 'Name', 'Hungary');
}
</script>
</head>
<body xmlns="javascript:Sys">
The country of the day is
<span innertext="binding {{translate()}}">Translate name</a>
<a href="#" onclick="translate()">Translate name</a>
</body>
```

![](img/b5597c749e848b27b0d305153ae16106_915_0.png)

You can also source the property to the window object to access global variables:

var today = new Date().format('D');
<span innertext="binding binding Name, source={{today}}"></span>

```
Code file [3-AjaxLibrary/12TopLevelBinding.htm] available for download at Wrox.com
```

```
Code file [3-AjaxLibrary/12TopLevelBinding.htm] available for download at Wrox.com
```

After clicking the "Translate name" link, the page gets updated, and the image shown in Figure 19-9 is rendered.

![](img/b5597c749e848b27b0d305153ae16106_915_1.png)

FIGURE 19-9: Using top-level binding

## Two-Way Binding

It often happens that you not only want to display data on the UI, but also want to change the data, and write it back to the source. The live binding syntax supports two-way binding, which means you do not have to write code to implement this feature. You can express it declaratively. The behavior can be set on the mode parameter of the binding expression using the `Sys.BindingMode`...

```
<input type="text" sys:value="binding Name, source={{data }}, mode=oneWay}/>
```

![](img/b5597c749e848b27b0d305153ae16106_915_2.png)

Remember that the default behavior is for Sys.BindingMode.auto to use two-way binding if the target is an input, select, or textarea element, or a component that implements the Sys INotifyPropertyChanged interface; otherwise it is one-way. Because you most likely create input controls to query by the user, and you need two-way binding for that, in most cases, you will not change the default, which means you can use the mode parameter.

Using two-way binding, you can bind the value of a textbox to a global variable (username) and display the global value with a span:

```
Please enter your name:
<input type="text">
sys:value=" binding username, source=(\{ window })"/>
<br />
Hello
<span sys:innertext="binding username, source=(\{ window })">
```

Code file 3-[AjaxLibrary/13-TwoWayBinding.html] available at Wrox.com

Two-way binding also opens the door for many useful element-driven scenarios. For example, you can bind a UI element's property to another UI element. In the example, you can see a textbox and a checkbox, and the checked property of the checkbox is bound directly to the disabled property of the textbox, the user must clear the checkbox to enable:

```
<input type="text"
id="txt"
sys:value="binding username, source=(\{ window })"
sys:disabled="binding checked, source=(\{ chk })"
<input type="checkbox" id="chk" />
<label for="chk">Disable editing</label>
```

Code file 3-[AjaxLibrary/13-TwoWayBinding.html] available at Wrox.com

The entered name is displayed on the page when the user navigates away from the textbox (input control loses focus), as shown in Figure 19-10.

![](img/b5597c749e848b27b0d305153ae16106_916_0.png)

## Custom Converters

If you are familiar with Windows Presentation Foundation (WPF), you have probably realized the similarities between the WPF data-binding syntax and the live binding in the Ajax Library. Another common point is the use of converters.

If you have a data source and want to bind its value to a UI element's property, it can happen that they have different types. If it happens anywhere you would probably cast your data value to the property's type, or use a helper function to resolve the data type mismatch. The concept of converters helps you to implement this.

In addition to the source and mode parameters, the live binding syntax lets you specify a convert and a convert back function. The convert back function is called when the data flows from the target to the source.

However, there is still a type mismatch between the string value and the Boolean properties. To overcome this, a custom function called disabledConverter is created. It is configured as a convert back method so the template engine will call it when the value of the target (textbox) is transferred to the source.

The following markup renders a textbox and a disabled button. The goal is to enable the button only if the user enters "I Accept":

```
<input type="text"
sys:value={ binding,
source={{ btn }}},
mode=OneWayToSource,
convertBack=disabledConverter,
expectedResult=I Accept />

<br />
<input type="button"
id="btn"
value="Submit " />
```

Code file [3-AjaxLibrary\14-Converters.htm] available for download at Wrox.com

As you can see from the syntax, button's disabled property (source) is bound to the value of the textbox (target). By default the binding would be two-way, but the behavior is changed to OneWayToSource because you would not want to display the disabled property (true or false) in the textbox. You ensure that the data flows from the textbox to the button.

The disabledConverter function is implemented with nothing special about this situation, so you can easily reuse it anywhere in your code.

```javascript
Sys.converters.disabledConverter = function(value, binding)
{
    return (value != binding.expectedResult);
}
```

Figure 19-11 shows the result page.

One thing to note is that the "I Accept" value is not hard-coded into the converter, but rather it is passed as a parameter. You can add additional parameters to your binding syntax, and all of them will be added as expanding properties.

![](img/b5597c749e848b27b0d305153ae16106_917_0.png)

FIGURE 19-11: The button is disabled with live binding
