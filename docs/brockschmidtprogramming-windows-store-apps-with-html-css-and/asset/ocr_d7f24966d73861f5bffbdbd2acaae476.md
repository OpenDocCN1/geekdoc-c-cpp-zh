+   - **debugBreakOnRender** Executes a `debugger` statement whenever the template is first rendered and especially gives you a hook into a compiled template (see below). This is especially helpful when a template's `render` call is being made implicitly from within another control like the `ListView`.
+   - **disableOptimizedProcessing** Turns off template compiling; see below.
+   - **extractChild** If set to `true`, suppresses creation of a containing `div` for the template contents, as discussed in the previous section. The default is `false`.

All of these except for `href` can be accessed at run time through properties on the control of the same names: `bindingInitializer`, `debugBreakOnRender`, `disableOptimizedProcessing`, and `extractChild`.58 Note that changing any of these properties at run time will reset the template and cause it to be recompiled the next time it's used.

Related to the behavior of the `extractChild` option is a second argument to the `render` method. If you already have a container into which you want the template contents rendered, you can provide it through this argument. For example, with `extractChild` set to `true`, the following code in scenario 3 of the modified Declarative binding sample (in the companion content) produces the same result as the default behavior (js/3_TemplateControlHRef.js):

```
this.sourceObjects.forEach(function (o) {
    var container = document.createElement("div");
    WinJS.Utilities.addClass(container, "win-template win-disposable");
    renderHere.appendChild(container);
    templateControl.render(o, container);
});
```

Such code gives you complete control over the kind of container element that's created for the template, if you have need of it.

As for `disableOptimizedProcessing` and `debugBreakOnRender`, these relate to a significant change for WinJS 2.0 (in Windows 8.1): template compilation. In WinJS 1.0, template rendering is always done in an interpreted manner, meaning that each time you rendered a template, WinJS would parse your template's markup and create each element in turn. You could improve this process by creating a rendering function directly, but you then lost the advantages of declarative markup.

To improve performance of declarative templates, especially with the ListView control, WinJS 2.0 compiles each template upon first rendering. This dynamically creates a rendering function that makes subsequent use of the template much faster. In fact, if you have a Windows 8 (WinJS 1.0) app that uses the `ListView` control and you simply migrate the project to Windows 8.1 (WinJS 2.0), you'll probably find it performing much better than before with no other changes.

Of course, with such extensive restructuring of the template engine there's always the possibility

58 One other property called `isDeclarativeControlContainer` is always set to `true`, and as with all other WinJS controls, the template has an `element` property that contains its root element in the DOM.