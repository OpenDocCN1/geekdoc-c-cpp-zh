
constructor, configuring properties and listeners as desired, and adding the element to the DOM wherever it's needed. Nothing new here at all where Store apps are concerned.

For examples of creating and using these controls, refer to the [HTML essential controls sample](#) in the Windows SDK, from which the images in Figure 5-1 and Figure 5-2 were obtained. In the sample you'll find different scenarios that show many variations for the individual controls, including styling options as I'll summarize later in the chapter. Note also that scenario 13 shows how to layout a form, and all the scenarios provide a radiobutton to toggle between the light and dark stylesheets (modifying the CSS links as discussed in Chapter 3). Scenario 14 lets you also see how this looks on any page background color of your choice.

**Tip** For more on creating, validating, and submitting forms built with HTML controls, refer to the [HTML5 form validation sample](#).

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_231_0.png)

**FIGURE 5-1** Standard HTML5 controls with default "light" styles (the ui-light.css stylesheet of WinJS).

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_232_0.png)

FIGURE 5-2 Standard HTML5 text input controls with default "light" styles (the ui-light.css stylesheet of WinJS).

| Control | Markup | Common Option Attributes | Element Content (inner text/HTML) |
|---|---|---|---|
| Button | <button type="button"> | (note that without type, the default is "submit") | button text |
| Button | <input type="button"> <input type="submit"> <input type="reset"> | value (button text) | n/a |
| Checkbox | <input type="checkbox"> | value, checked | n/a (use a label element around the input control to add clickable text) |
| Drop Down List | <select> | size="1" (default), multiple, selectedIndex | multiple <option> elements |
| Email | <input type="email"> | value (initial text) | n/a |
| File Upload | <input type="file"> | accept (mime types), multiple | n/a |
| Hyperlink | `<a>` | href, target | Link text |
| ListBox | `<select>` with size > 1 | size (a number greater than 1), multiple, selectedIndex | multiple `<option>` elements |
| Multi-line Text | `<textarea>` | cols, rows, readonly, data-placeholder (because placeholder has a bug) | initial text content |
| Number | `<input type="number">` | value (initial text) | n/a |
| Password | `<input type="password">` | value (initial text) | n/a |
| Phone Number | `<input type="tel">` | value (initial text) | n/a |
| Progress | `<progress>` | value (initial position), max (highest position; min is 0), no value makes it indeterminate | n/a |
| Radiobutton | `<input type="radio">` | value, checked, defaultChecked | radiobutton label |
| Rich Text | `<div>` | contentEditable="true" | HTML content |
| Slider | `<input type="range">` | min, max, value (initial position), step (increment) | n/a |
| URI | `<input type="url">` | value (initial text) | n/a |

**When to show progress controls?** A `progress` element is clearly intended to inform the user that something is happening in the app. They can be used to indicate background progress, like syncing, or to indicate that some processing is blocking further interactivity. The latter case is best avoided entirely, if possible, so that the app is always interactive. If you must block interactivity, however, the recommendation is to show a progress indicator after two seconds and then provide a means to cancel the operation after ten seconds.

## Extensions to HTML Elements

As you probably know already, there are many developing standards for HTML and CSS. Until these are brought to completion, implementations of those standards in various browsers are typically made available ahead of time with vendor-prefixed names. In addition, browser vendors sometimes add their own extensions to the DOM API for various elements.

With Windows Store apps, of course, you don't need to worry about the variances between browsers, but because these apps essentially run on top of the Internet Explorer engine, it helps to know about those extensions that still apply. The key ones are summarized in the table below, and you can find the full details in the [Elements]() and [Cascading Style Sheets]() references in the documentation. We'll also encounter a few others in later chapters. Another simple way to determine what extensions are available on any given object is to examine that object directly in the Visual Studio debugger at run time. Visual Studio will show the properties directly; expand the object's Methods node to see all the
functions it supports, and expand its styles node for style-related properties.

If you've been working with HTML5 and CSS3 in Internet Explorer already (especially Internet Explorer 9), you might be wondering why the table doesn't show the various animation (msAnimation*), transition (msTransition*), and transform properties (msPerspective* and msTransformStyle), along with msBackfaceVisibility and msFlex* (among others). This is because these standards are now far enough along that they no longer need vendor prefixes with Internet Explorer 10+ or Store apps (though the ms* variants still work).

| Methods | Description |
|---|---|
| msMatchesSelector | Determines if the control matches a selector. |
| msSetPointerCapture, msGetPointerCapture, msReleasePointerCapture | Captures, retrieves, and releases pointer capture for an element. |
| msZoomTo | Scrolls or zooms an element to a given coordinate with animation. |

| Style properties (on element.style) | Description |
|---|---|
| msGrid*, msRow* | Gets or sets placement of element within a CSS grid. |
| msContentZoom*, msContentZooming | Enables programmatic control of zooming; see Touch Zooming and Panning. |
| msScroll*, msOverflowStyle | Enables programmatic control of panning and scrollbar styling; see Touch Zooming and Panning. |
| msTouchAction | Specifies whether a given region can be zoomed or panned |
| msTouchSelect | Toggles the “gripper” visuals that enable touch text selection. |
| msUserSelect | When set to ‘element’ allows the element to be selected; ‘text’ allows inline selection of the element’s contents; the default is ‘none’. Note that this replaces an earlier data-win-selectable attribute from early developer previews of Windows 8. |

| Events (add "on" for event properties) | Description |
|---|---|
| mscontentzoom | Fires when a user zooms an element (Ctrl + /-, Ctrl + mousewheel), pinch gestures. |
| msgesture[change | end | hold | tap | pointercapture] | Gesture input events (see Chapter 12, "Input and Sensors"). |
| msinertialstart | Gesture input events (see Chapter 12). |
| msgotpointercapture, mslostpointercapture | Element acquired or lost capture (set with msSetPointerCapture). |
| mspointer[cancel | down | enter | leave | move | out | over | up] | Pointer input events (see Chapter 12). |
| msmmanipulationstatechanged | State of a manipulated element has changed. |

## WinJS Controls

Windows defines a number of controls that help apps fulfill various design guidelines. As noted before, these are implemented in WinJS for apps written in HTML, CSS, and JavaScript, rather than WinRT; this allows those controls to integrate naturally with other DOM elements. Each control is defined as part of the `WinJS.UI` namespace using `WinJS.Class.define`, where the constructor name matches the control name. So the full constructor name for a control like the Rating is `WinJS.UI.Rating`. As noted before in the control model, this is the name you specify within a `data-win-control` attribute for the control's root element such that `WinJS.UI.process/processAll` can instantiate that control.

**Tip** Once a WinJS control is instantiated, the root element object will have a `winControl` property attached to it. This `winControl` object is the result of calling `new` on the control's constructor and gives access to the control's specific methods, properties, and events. The `winControl` object also has an `element` property to go the other direction.

The simpler UI controls are `BackButton`, `DatePicker`, `Rating`, `TimePicker`, and `ToggleSwitch`, the default styling for which are shown in Figure 5-3. I trust that the purpose of each control is obvious!

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_235_0.png)

**FIGURE 5-3** Default (light) styles for the simple WinJS controls.

There are then three other WinJS controls whose purpose is to contain other content and provide some other behavior around it. These are `HtmlControl`, `Tooltip`, and `ItemContainer`.

The `HtmlControl` is a simpler form of the page controls we saw in Chapter 3, allowing you to easily load some HTML fragment from your app package (along with its referenced CSS and JavaScript) as a

47 There is also the `WinJS.UI.TabContainer` control that is primarily used within the ListView control implementation. It has limited direct utility for apps and does not support declarative processing, so I won't talk more of it here.
