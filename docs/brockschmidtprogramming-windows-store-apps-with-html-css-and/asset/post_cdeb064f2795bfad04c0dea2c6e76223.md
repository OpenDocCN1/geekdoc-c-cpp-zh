
```css
#createNavBar .win-navbar {
  border-top: 10px solid #008299;
}
```

Within the NavBar, any of your own child elements (like the TRAVEL and FEATURED labels in the Travel app) have whatever classes you assign to them. If you have NavBarContainer elements, those are composed of a considerable hierarchy of parts:

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_488_0.png)

To color the page indicators like the Travel app, for example, uses these rules:

```css
#createNavBar .win-navbarcontainer-pageindicator {
  background-color: #636363;
}

#createNavBar .win-navbarcontainer-pageindicator-current {
  background-color: #008299;
}
```

The viewport and pageindicator-box (if I may drop the win-navbarcontainer- prefix) are sibling elements, each of which has its own portion within the container where you can style background colors, margins/padding, etc.

Within the viewport we then have the pannable surface area alongside the left and right navigation arrows. The navarrow style specifically styles the arrow inside the buttons; the navleft and navright selectors (including pseudo-styles) affect the surrounding controls.

Within the win-navbarcontainer-surface element is where you’ll find the NavBarCommand elements, each of which has this hierarchy of elements and classes, through which you can specifically address whichever part you want:

```
<div class="win-navbarcommand">
  <div class="win-navbarcommand-button">
    <div class="win-navbarcommand-content">
      <div class="win-navbarcommand-icon"></div>
      <div class="win-navbarcommand-label"></div>
    </div>
    <div class="win-navbarcommand-splitbutton"></div>
  </div>
</div>
```

Alternately, you might find it easier to provide a template for the command items so that you can control the elements that are built up for each one.

As for the little triangle that you see on the secondary flyout in the Travel app (to point up to the Destinations button), that's just a little element in the Flyout that uses a background-image; it's not part of the NavBarContainer with the list of items.

## Flyouts and Menus

Going back to our earlier discussion about where to place commands, a flyout control—WinJS.UI.Flyout—is used for confirmations, collecting information, and otherwise answering questions in response to a user action. The menu control—WinJS.UI.Menu—is then a particular kind of flyout that contains WinJS.UI.MenuCommand controls rather than arbitrary HTML. In fact, Menu is directly derived from Flyout using WinJS.Class.define, so they share much in common. As flyouts, they also share some feature in common with the app bar and nav bar, as all of them, in fact, derive from a common internal base class (WinJS.UI._Overlay).

Tip In addition to the Flyout control that you'll employ in an app, there is also a system flyout that appears in response to some API calls, such as creating or removing a secondary tile (see Chapter 16, specifically Figure 16-5 and the "Secondary Tiles" section). Although visually the same, the system flyout will trigger a blur event to the app whereas the WinJS flyout, being part of the app, does not. As a result, a system flyout will cause a non-sticky app bar to be dismissed. To prevent this, it's necessary to set the appbar's sticky property to true before calling APIs with system flyouts. This is demonstrated in scenario 7 of the Secondary tiles sample.

Styling in Blend As with app bars and nav bars, you can right-click a flyout element in Blend's Live DOM and select Activate Flyout to make it visible for styling, or you can activate it in Interactive Mode and switch back to Design Mode. To work with it in Visual Studio's debugger or the DOM Explorer, you'll need to make it sticky, otherwise switching to Visual Studio will dismiss it.

Before we look at the details, let's see a number of visual examples from the HTML flyout control sample in which we already saw a popup menu on an app bar command. The Flyout controls used in scenarios 1-4 are shown in Figure 9-1 (on the next page). Notice the variance of content in the flyout itself and how the flyout is always positioned near the control that invoked it, such as the Buy, Login, and Format output text buttons and the *Lorem ipsum* hyperlink text. These examples illustrate that a flyout can contain a simple message with a button (scenario 1, for warnings and confirmations), can contain fields for entering information or changing settings (scenarios 2 and 3), and can have a title (scenario 4). Scenario 5, for its part, contains the example of a popup header menu with *Menu* that we'll see a little later.

There are two key characteristics of flyout controls, including menus. One is that flyouts can be dismissed programmatically, like an app bar, when an appropriate control within the flyout is invoked. This is the case with the Complete Order button of scenario 1 and the Login button of scenario 2.

The second characteristic, also shared with the app bar, is the light dismiss behavior: clicking or tapping outside the control dismisses it, as does the ESC key, which means light dismiss is the equivalent of pressing a Cancel or Close button in a traditional dialog box. The benefit here is that we don't need a visible button for this purpose, which helps simplify the UI. At the same time, notice in scenario 3 of Figure 9-1 that there is no OK button or other control to confirm changes you might make in the flyout. With this particular design, changes are immediately applied such that dismissing the flyout does not reverse or cancel them. If you don't want that kind of behavior, you can place something like an Apply button on the flyout and not make changes until that button is pressed. In this case, dismissing the flyout would cancel the changes.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_490_0.png)

**Figure 9-1** Examples of flyout controls from the HTML flyout control sample.

I'll again encourage you to read the *Guidelines and checklist for Flyouts* topic that goes into detail about how and when to use the different designs that are possible with this control. It also outlines when not to use the control: for example, don't use flyouts to surface errors not related to user action (use a message dialog instead), don't use them for primary commands (use the app bar), don't use them for text selection context menus, and avoid them for UI that is part of a workflow and should be directly on the app canvas. These guidelines also suggest keeping a flyout small and focused (omitting unnecessary controls) and making sure a flyout is positioned close to the object that invoked it. Let’s now see how that works in the code.

### WinJS.UI.Flyout Properties, Methods, and Events

Most of the properties, methods, and events of the `WinJS.UI.Flyout` control are exactly the same as we’ve already seen for the app bar. The `show` and `hide` methods control its visibility, a `hidden` property indicates its visible state, and the same `beforeshow`, `aftershow`, `beforehide`, and `afterhide` events fire as appropriate. The `afterhide` event is typically used to detect dismissal of the flyout.

Like the app bar, the flyout also has a `placement` property, but it has different values that are only meaningful in the context of the flyout’s own `alignment` and `anchor` properties. In fact, all three properties are optional parameters to the `show` method because they determine where, exactly, the flyout appears on the screen; the default `placement` and `alignment` can also be set on the control itself because these are optional with `show`. (Note also that if you don’t specify an `anchor` in the `show` method; the `anchor` property must already be set on the control or `show` will throw an exception.)

The `anchor` property identifies the control that invokes the flyout or whatever other operation might bring up a flyout (as for confirmation). The `placement` property (a string) then indicates how the flyout should appear in relation to the `anchor`: `top`, `bottom`, `left`, `right`, or `auto` (the default). Typically, you use a specific `placement` only if you don’t want the flyout to possibly obscure important content. Otherwise, you run the risk of the flyout element being shrunk down to fit the available space. The flyout’s `content` will remain the same size, mind you, so it means that—ick!—you’ll get scrollbars! So, unless you have a really good reason and a note from your doctor, stick with `auto` placement so that the control will be placed where it can be shown full size. Along these same lines, if you’re supporting the 320px minimum width, limit your flyouts also to that size.

The `alignment` property, for its part (also a string), when used with a `placement` of `top` or `bottom`, determines how the flyout aligns to the edge of the `anchor`: `left`, `right`, or `center` (the default). The content of the flyout itself is aligned through CSS as with any other HTML.

If you need to style the flyout control itself, you can set styles in the `win-flyout` class, like fonts, default alignments, margins, and so on. As with other WinJS style classes like this, use `win-flyout` as a basis for more specific selectors unless you really want to style every flyout in the app. Typically you also exclude `win-menu` from the rule so that menu flyouts aren’t affected by such styling. For example, most of the scenarios in the HTML flyout control sample have rules like this:

```css
.win-flyout:not(.win-menu) button,
.win-flyout:not(.win-menu) input[type="button"] {
    margin-top: 16px;
    margin-left: 20px;
    float: right;
}
```
