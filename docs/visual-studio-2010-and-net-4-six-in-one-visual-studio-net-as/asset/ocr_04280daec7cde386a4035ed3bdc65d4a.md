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

+   - countries.beginUpdate();
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
    <span>{ binding Name }</span>
    <span>{ binding Capital }</span>
  </li>
</ul>
```

Code file [3-AjaxLibraryII-LiveBinding.htm] available for download at Wrox.com

As you can see in this example, you use the binding markup extension, and then the name of the property you want to display. These placeholders will be automatically updated when the source data changes. However, note that you must always modify your data source via the Sys.Observer methods. If you modify the data source directly, without going through the interface, notification events will not be raised.