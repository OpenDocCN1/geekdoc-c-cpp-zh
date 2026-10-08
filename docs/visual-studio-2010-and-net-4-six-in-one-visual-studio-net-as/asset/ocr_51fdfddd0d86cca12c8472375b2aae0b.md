Although, theoretically, you could choose any name for this CSS class, the sys-template is not only a naming convention, it is mandated by the template engine.

Any attribute that begins with the dv prefix sets a property of the DataView control. The data property is set to bound the data that is be rendered by control. (It is very similar to the DataSource property of server-side controls).

Within the template, you use the {{ }} syntax to mark the placeholders where the values should be rendered. Between the double curly braces, you can write any expression that will be evaluated in JavaScript. The expression will be evaluated in the context of the data item. In this case, you can directly refer to any property of the current record in the data source. You can add the {{ }} expression to the markup without wrapping it in an HTML tag, but you can also bind it to an attribute of. If bound to an HTML attribute, then you must prepend the sys: prefix to it, as you can see at the sys:src attribute of the img tag in this example.

For an ASP.NET developer, the {% Name %> expression is very similar to the <% Eval(Name) %> server-side expression. However, later in this chapter, you will see the client version is more powerful because it integrates the more mature data-binding features of Windows Presentation Foundation (WPF).

This declarative markup renders a bulleted list in the browser, as shown in Figure 19-4.

+   * Austria (Vienna)
* Australia (Canberra)
* Brazil (Berlin)
* Czech (Prague)
* Spain (Madrid)
* India (Delhi)
* Greece (Athens)
* Hungary (Budapest)
* Sweden (Stockholm)
* Slovakia (Bratislava)
* United Kingdom (London)
* United States (Washington, D.C.)

FIGURE 19-4: Bulleted list rendered by the DataView control

The previous code shows the declarative way of using the DataView control. If you want to separate the markup and the logic, you have the option of creating the DataView imperatively. In this case, you can clean up the markup and remove all the DataView-related settings:

```
<body xmlns:javascript="Sys">
  <ul class="sys-template">
    <li>
      {{ Name }}
      <img src:sys='{{../images/’ + Code + '.gif'}} />
    </li>
  </ul>
</body>
```

Code file [3-AjaxLibrary\04-DataViewDeclarative.htm] available for download at Wrox.com

The DataView can be instantiated, configured, and attached with a single line of code — for example, in the pageLoad handler:

```
function pageLoad() {
{
    data: countries
  }}
}
```

Code file [3-AjaxLibrary\05-DataViewFromCode.htm] available for download at Wrox.com