
Although sourceProperty is what's present in the data-win-bind attribute, you're free to wire up to any other property you want to include in the relationship. The code above, for example, will be called with sourceProperty equal to [color], but it doesn't actually bind to that directly. It instead uses a binding descriptor with winJS.Binding.bind to hook up the setBackColor handler to three separate color subproperties. Although setBackColor is used for all three, you could just as easily have separate handlers for each one if, for example, each required a unique conversion.

Ultimately, what's important is that the handler given to the source.bind method performs an appropriate update on the target object. In the code above, you can see that setBackColor sets dest.style.backgroundColor.

Hmmm. Do you see a problem there? Try changing the last data-win-bind attribute in html/1_BasicBinding.html to set the text color instead:

```
data-win-bind="style.color : color BasicBinding.toCssColor"
```

Oops! It still changes the background color! This is because the initializer isn't honoring destProperty, and that would be a difficult bug to track down when it didn't work as expected. Indeed, because the initializer pays no attention to destProperty you can use a nonexistent identifier and it will still change the background color:

```
data-win-bind="some.ridiculous.identifier : color BasicBinding.toCssColor"
```

Technically speaking, then, we could rewrite the code as follows:

```
dest.[destProperty[0]][destProperty[1]] =
rgb(source.color.red, source.color.green, source.color.blue);
```

Even this code makes the assumption that the target path has only two components—to be really proper about it, you need to iterate through the array and traverse each step of the path. Fortunately, WinJS.Utilities.getMember is a helper for just that purpose, though to do an assignment you need to pop the last property from the array so that you can use [ ] to reference it:

```
var lastProp = destProperty.pop();
var target = destProperty.length ?
WinJS.Utilities.getMember(destProperty.join("."), dest) : dest;
destProperty.push(lastProp);

function setBackColor() {
target[lastProp] = rgb(source.color.red, source.color.green, source.color.blue);
}
```

This code can be found in the modified Declarative binding sample in this chapter's companion content. Note that I'm building that reference outside of the setBackColor handler because there's no need to rebuild it every time a source property changes. Also, calling push to restore destProperty is important in scenario 3 when this initializer is used with a template that's rendered multiple times on the same page. In that case the destProperty array is used with each call to the initializer, meaning that we don't want to make any permanent changes.

Remember also that `sourceProperty` can also contain multiple parts, so you may need to evaluate that path as well. The sample gets away with ignoring `sourceProperty` because it knows it's only using the `toCssColor` initializer with `source.color` to begin with. Still, if you're going to write an initializer, best to make it as robust as you can! Again, you can use `getMember` to assemble the reference you need, and because you're just retrieving the value, you can do it in one line:

```
var value = WinJS.Utilities.getMember(sourceProperty.join("."), source);
```

## Binding Templates

Now that we understand how controls work from Chapter 5 and how data binding works to populate those controls from a data source, the next question to ask is how we might define reusable pieces of HTML that also integrate declarative data binding.

There are two ways to do this. First, you can certainly use `data-win-bind` syntax within an `HtmlControl` or a custom control (remembering to bind control properties through `WinControl` rather than the root element). Once the control is instantiated with `WinJS.UI.processAll()`, you can then call `WinJS.Binding.processAll()` to bind each element to an appropriate source.

The second way is through the `WinJS.Binding.Template` control. It provides a way to define an HTML snippet, either inline or in a separate HTML file, and then render that snippet, however many times you want, with whatever data source you need for each rendering. The template makes the call to `Binding.processAll()` automatically and provides some other options where binding is concerned.

To define a template control, first create a `div` with `data-win-control = "WinJS.Binding.Template"` and `data-win-options` string, if needed. The contents of the template—what will be copied into the DOM when you render the template—can then be defined either inline or in a separate file. In that markup you're free to use whatever controls you want along with `data-win-bind` attributes.

**Tip** Blend for Visual Studio 2013 has some helpful features to easily create templates and data bindings from a data source for WinJS collection controls. We'll see this in Chapter 7.

Here's an example from scenario 2 of the modified Declarative binding sample in this chapter's companion content (html/2_TemplateControl.html, where the `toCssColor` initializer is corrected as we did earlier for scenario 1):

```
<div id="templateControlTemplate" data-win-control="WinJS.Binding.Template">
    <!-- Bind both the background and the aria-label HTML attribute for the div -->
    <div class="templateControlRenderedItem"
        data-win-bind="style.background: color TemplateControl.toCssColor;
            this['aria-label']: text WinJS.Binding.setAttribute" role="article">
        <ol>
            <li data-win-bind="textContent: text"></li>
<li><span class="templateControlTemplateLabel">r:</span><span data-win-bind="textContent: color.r"></span></li>
<li><span class="templateControlTemplateLabel">g:</span><span data-win-bind="textContent: color.g"></span></li>
<li><span class="templateControlTemplateLabel">b:</span><span data-win-bind="textContent: color.b"></span></li>
        </ol>
    </div>
</div>
```

Scenario 3 of the example, which is an addition I've made to the original sample, has the same template contents stored in html/3_TemplateContents.html (<!DOCTYPE html>, <html>, and <body> tags are optional and have no effect). We then refer to those contents with the control's href option in data-win-options (html/3_TemplateControl.html):

```
<div id="templateControlTemplate" data-win-control="WinJS.Binding.Template"
data-win-options="{ href : '/html/3_TemplateContents.html' }">
</div>
```

Note Using the href option disables certain optimizations with templates that otherwise dramatically improve performances. You should only use href, then, when absolutely necessary.

What's unique about this control is that it automatically hides itself (setting style.display="none") inside its constructor so that its contents never appear in your layout. You can confirm this when you run scenarios 2 or 3 of the example—If you expand everything in Visual Studio's DOM Explorer, you won't be able to find the template control anywhere. The control instance, however, is still in memory: a quick getElementById or querySelector will get you to the hidden root element, and that element's winControl property is where you'll find the WinJS template object.

That object has a number of methods and properties that we'll return to in a bit. The most important of these is the asynchronous render method. Given whatever data source you want to bind to, render returns a promise that's fulfilled with a copy of the template's contents in a new element, where Binding.processAll has already been called with the data source. You can then attach that element to the DOM wherever you'd like.

Scenario 2 of the example, for instance, renders the template three times, binding each to a different source object that contains text and a color. First, in html/2_TemplateControl.html, the target div for the rendered templates is initially empty:

```
<div id="templateControlRenderTarget"></div>
```

In js/2_TemplateControl.js, we define the observable data sources as follows (showing WinJS.Binding.define):

```
var DataSource = WinJS.Binding.define({
  text: "", color: { r: 0, g: 0, b: 0 }
});

// In the page control's init method
```
