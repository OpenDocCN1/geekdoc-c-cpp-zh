```
~~~html
<div id="header" data-win-control="WinJS.UI.HtmlControl"
    data-win-options="{uri: '/sample-utils/header.html'}"></div>
<div id="content">
    <h1 id="featureLabel"></h1>
    <div id="contentHost">
        <!-- Sample-specific content -->
    </div>
</div>
<div id="footer" data-win-control="WinJS.UI.HtmlControl"
    data-win-options="{uri: '/sample-utils/footer.html'}"></div>
~~~
```

This uses two HtmlControl instances for static header and footer content, while the sample's JavaScript builds up its scenario selectors within the contentHost element. Clearly, each HtmlControl allows the app to keep certain content isolated in separate files; in the case of the SDK samples, it makes it very easy to globally update the headers and footers of hundreds of samples.

# ## Example: WinJS.UI.Rating (and Other Simple Controls)

For starters, here's some markup for a WinJS.UI.Rating control, where the options specify two initial property values and an event handler:

```
~~~html
<div id="rating1" data-win-control="WinJS.UI.Rating"
    data-win-options="{averageRating: 3.4, userRating: 4, onchange: changeRating}">
</div>
~~~
```

To instantiate this control, we need either of the following calls:

```
~~~javascript
WinJS.UI.process(document.getElementById("rating1")); //Or any ancestor element
WinJS.UI.processAll();
~~~
```

Again, both of these functions return a promise, but it's unnecessary to call then/done unless we need to do additional post-instantiation processing or handle exceptions that might have occurred (and that are otherwise swallowed). Also, note that the changeRating function specified in the markup must be globally visible and marked for processing, or else the control will fail to instantiate.

Alternatively, we can instantiate the control and set the options procedurally. In markup:

```
~~~html
<div id="rating1" data-win-control="WinJS.UI.Rating"></div>
~~~
```

And in code:

```
~~~javascript
var element = document.getElementById("rating1");
WinJS.UI.process(element);
element.winControl.averageRating = 3.4;
element.winControl.userRating = 4;
element.winControl.onchange = changeRating;
~~~
```

The last three lines above could also be written as follows using the WinJS.UI.setOptions method, but this isn't recommended because it's harder to debug:

```
~~~javascript
var options = { averageRating: 3.4, userRating: 4, onchange: changeRating };
WinJS.UI.setOptions(element.winControl, options);
~~~
```