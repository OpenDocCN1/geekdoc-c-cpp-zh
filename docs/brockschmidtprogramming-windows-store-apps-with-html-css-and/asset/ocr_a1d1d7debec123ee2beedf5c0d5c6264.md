Take note that the `NavBarContainer` works directly with a `Binding.List` (not its `dataSource`) and is thus limited to in-memory collections.

The `NavBarContainer` also supports these additional members:

+   - `template` (Property) Gets or sets a `WinJS.BindingTemplate` or rendering function that creates the DOM for each item in the data collection. The template must render a single root element but can otherwise contain whatever controls you'd like.
+   - `layout` (Property) A value from the `WinJS.UT.Orientation` enumeration, either `horizontal` (the default) or `vertical`. The horizontal layout works with paging, as we've seen, with the `maxRows` property (default is 1) controlling the layout in each page. The vertical layout pans continuously without page indicators or arrows and ignores `maxRows`.
+   - `currentIndex` (Property) Gets or sets the index of the item with the keyboard focus.
+   - `fixedSize` (Property) When `true`, the width of each command in the container is determined by its styling, which means there could be gaps on the sides. When `false` (the default), the container will size the commands so that they fill the horizontal width of the container.
+   - `forceLayout` (Method) As with other collection controls, call this when making the control visible again after changing its `display` style to something other than `none`.
+   - `invoked` (Event) Fired when a command in the container has been invoked in response to a click, tap, or the Space or Enter keys being pressed. The `eventArgs.detail` object contains the `index` and `navbarcommand` object of the command that was invoked, along with the `data` item that was used to create the command. Note that navigation to the command's `location` will have already started when this event is fired.
+   - `splitToggle` (Event) Fired when a command with `splitButton: true` changes its `splitOpen` state. The `eventArgs.detail` object contains the same properties as `invoked` above plus the new state in the `opened` property. You use this to show or hide a secondary `NavBarContainer`.

The `layout` and `fixedSize` properties are demonstrated in scenario 3 of the HTML NavBar control sample. By default it uses dynamic width, so both containers will fill the width:

![](bbox=[0.15, 0.761, 0.655, 0.891])