
control. The `WinJS.UI.HtmlControl` constructor, in fact, simply calls `WinJS.UI.Pages.render`, loading that content into the control. Indeed, page controls themselves can be used in the same way: you can, for example, load up multiple page controls within the same host page. I prefer to keep these ideas separate, however, using page controls for full-page DOM replacement and the `HtmlControl` for control-like fragments.

Because the purpose of the `HtmlControl` is to simply encapsulate other pieces of HTML, the control itself has no inherent visuals or styling. If you want an example, simply look at the header and footer of any Windows SDK sample!

The `Tooltip` control, for its part, is a step above the plain text tooltip that HTML provides automatically for the `title` attribute. Its behavior is such that when you attach it to some other control, it will appear automatically for hover states. With default styling and text, it appears just like the default tooltips (I've cropped the button to which the tooltip is attached; it's not part of the tooltip):

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_236_0.png)

Unlike the default tooltip, however, the `WinJS.UI.Tooltip` control can use any HTML including other controls. We'll see this shortly in the section "Example: `WinJS.UI.Tooltip`." The default rectangle shape can also be fully styled, but I'll also make you wait for that!

The `ItemContainer` control is also a container (as befits its name) for some other piece of HTML that acts as a single unit. The HTML within it can again include other controls, but the behaviors apply to the item as a whole. Those behaviors, as determined by various options, include swipe (to select), tap (to invoke), and HTML5 drag-and-drop support. Here's an example item in both selection states:

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_236_1.png)

We'll see more about these options a little later with specific examples.

As noted in this chapter's introduction, I'm saving other WinJS controls for later chapters because they each need additional context. We'll see the `Repeater` in Chapter 6; the `FlipView`, `ListView`, and `SemanticZoom` that work with collections are covered in Chapter 7; the `Hub` we'll see in Chapter 8 as it's pertinent to layout; `AppBar`, `NavBar`, and `Flyout` are transient commanding UI that we'll come to in Chapter 9 (because they don't participate in layout); and media controls and the `SearchBox` we'll encounter in Chapters 13 and 15, respectively. Much to look forward to!

Now to reiterate the control model, a WinJS control is declared in markup by attaching `data-win-control` and `data-win-options` attributes to some root element. That element is typically a `div` (block element) or `span` (inline element), because these don't bring much other baggage, but any element, such as a `button`, can be used. These elements can, of course, have `id` and `class` attributes as needed.

The available options for the WinJS controls we're discussing in this chapter are summarized in the table below. The table includes those events that can be wired up declaratively through the `data-win-options` string, if desired, or through JavaScript. For full documentation on all these options, start with the Controls list in the documentation and go to the control-specific topics linked from there, or use the links given below. For details on the syntax of the `data-win-options` string, see the next section in this chapter.

| Fully-qualified constructor name as used in data-win-options | Options in data-win-options<br>(note that event names use the 'on' prefix in the attribute syntax) |
| --- | --- |
| `WinJS.UI.BackButton`<br>(sample) | Events: none. The `BackButton` instead calls `WinJS.Navigation.back` directly when clicked or tapped (or the user presses Alt+Left) and listens for `WinJS.Navigation.onnavigated` to enable or disable itself appropriately, depending on the navigation stack.<br>Methods: `refresh` |
| `WinJS.UI.DatePicker`<br>(sample) | Properties: `calendar`, `current`, `datePattern`, `disabled`, `maxYear`, `minYear`, `monthPattern`, `yearPattern`<br>Events: `onchange` |
| `WinJS.UI.HtmlControl`<br>(see default HTML in any SDK sample) | Properties: `uri` (referring to an in-package fragment), such as `"/controls/mycontrol.html"`. |
| `WinJS.UI.ItemContainer`<br>(sample) | Properties: `draggable`, `selected`, `selectionDisabled`, `swipeBehavior`, `swipeOrientation`, `tapBehavior`<br>Events: `oninvoked`, `onselectionchanging`, `onselectionchanged`<br>Methods: `forceLayout` |
| `WinJS.UI.Rating`<br>(sample) | Properties: `averageRating`, `disabled`, `enableClear`, `maxRating`, `tooltipStrings` (an array of strings the size of `maxRating`), `userRating`<br>Events: `oncancel`, `onchange`, `onpreviewchange` |
| `WinJS.UI.TimePicker`<br>(sample) | Properties: `clock`, `current`, `disabled`, `hourPattern`, `minuteIncrement`, `minutePattern`, `periodPattern`. (Note that the date portion of `current` will always be July 15, 2011 because there are no known daylight savings time transitions on this day.)<br>Events: `onchange` |
| `WinJS.UI.ToggleSwitch`<br>(sample) | Properties: `checked`, `disabled`, `labelOff`, `labelOn`, `title`<br>Events: `onchange` |
| `WinJS.UI.Tooltip`<br>(sample) | Properties: `contentElement`, `innerHTML`, `infotip`, `extraClass`, `placement`<br>Events: `onbeforeclose`, `onbeforeopen`, `onclosed`, `onopened`<br>Methods: `open`, `close` |

**Note** All WinJS controls have the methods `addEventListener`, `removeEventListener`, `dispatchEvent`, and `dispose`, along with an `element` property that identifies the control's root element.

When setting WinJS control options from JavaScript, be sure to set them on the `winControl` object and not on the containing element itself. (This is very important to remember when doing data-binding to control properties, as we'll see in Chapter 6.) Event handlers can be assigned through `winControl.on<event>` properties or through `winControl.addEventListener`. If you want to set multiple options at the same time, you can use the `WinJS.UI.setOptions` method, which accepts the `winControl` object (not the root element) and a second object containing the options. Such an object is exactly what WinJS produces when it parses a `data-win-options` string.

## Sidebar: The Ubiquitous dispose Method

If you look at the documentation for any of these controls, you'll see that they each have a method named `dispose` whose purpose is to release any resources held by the control. In addition, every page control you define through `WinJS.UI.Pages.define` also has a `dispose` method. All together, these methods allow WinJS to make sure that the pages and the controls on those pages release any necessary resources when they're removed from the DOM (correcting memory leaks that were observed in Windows 8). That is, when you navigate away from a page, the `PageControlNavigator` we learned about in Chapter 3 calls the page's `dispose` method, which in turn calls `WinJS.Utilities.disposeSubTree` on its root element. That method calls `dispose` on every child control that is marked with the `win-disposable` class (as all WinJS controls are) and that has a `dispose` method (as all WinJS controls do).

If you are using `PageControlNavigator`, then, you don't need to worry much about calling `dispose` yourself. However, if you implement your own navigation controller or page-loading mechanism, be sure to replicate this behavior and call `dispose` on any controls that are being removed from the DOM. Additionally, custom controls should also implement a `dispose` method and mark themselves with the `win-disposable` class to participate in the process. Custom controls that can contain other controls (like a `ListView` or the `PageControlNavigator`) must also be mindful to manage control disposal. We'll talk more of this later with custom controls, but if you want a quick demonstration refer to the Dispose model sample.

## Syntax for data-win-options

As noted earlier, the `data-win-options` attribute is a string containing key-value pairs, one for each property or event, separated by commas, in the form `{ <key1>: <value1>, <key2>: <value2>, ... }`. When a control is instantiated through `WinJS.UI.processAll`, WinJS parses the options string into the equivalent JavaScript object and passes it to the control's constructor. Easy enough! (Remember to be mindful of syntax errors in your `data-win-options` string, though, because such errors will cause an app to abruptly terminate during control instantiation.)
