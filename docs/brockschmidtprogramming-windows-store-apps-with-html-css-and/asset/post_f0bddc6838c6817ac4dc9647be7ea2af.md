
An exception to this guidance for charms is Search (not shown). Apps that wish to have their content participate in global search, which includes web results, can work with the charm. Apps that need only provide in-app search capabilities should provide appropriate controls on-canvas or in an app bar or nav bar.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_457_0.png)

- Commands that can't be placed in Charms and don't need to be on the app canvas are then placed within the nav bar and app bar, as shown below in the Travel app. Both bars are invoked together by swiping in from either the top or bottom edges and are the closest analogies to traditional menus:
  - The top bar should contain navigation commands.
  - The bottom app bar contains all other commands that are sensitive to the context or selection, as well as global (nonselection) commands. Context and global commands are placed on different sides of the app bar.
  - App bar and nav bar commands can display menus to group related commands to reduce clutter; below, the Destinations button in the nav bar opens up the secondary list.

You see message dialogs. Note that a message dialog is used only when the app is in the foreground. Toast notifications, as we'll see in Chapter 16, "Alive with Activity," typically apply only to background apps.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_459_0.png)

- Finally, other errors that don't require user action can be displayed either inline (on the app canvas) or through flyouts. See Laying out your UI errors for full details; we'll see some examples later on as well.

Where the app bar (on the bottom) is concerned, it's also important to organize your commands into sets, as this streamlines implementation as we'll see in the next section. For full guidance I recommend Guidelines and checklist for app bars and Commanding Design in the documentation, which provide many specifics on placement, spacing, and grouping. That guidance can be summarized as follows:

- First, make two groups of commands: one with those commands that appear throughout the entire app, regardless of context, and another with those that show only on certain pages. The app bar control is fairly simple to reconfigure at run time for different groups.
- Next, create command sets, such as those that are functionally related, those that toggle view types, and those that apply to selections. Remember that an app bar command can display a popup menu, as shown below, to provide a list of options and/or additional controls, including longer labels, drop-down lists, checkboxes, radiobuttons, and toggle switches. In this way you can combine closely related commands into a single one that gets more room to play than its little space on the app bar proper.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_459_1.png)

- For placement, put persistent commands on the right side of the app bar and the most common context-specific commands on the left. After that, begin to populate toward the middle. This recommendation comes from the ergonomic realities of human hands: fingers and thumbs—even on the largest hands of basketball players!—grow only so long and can reach only so far on the screen without having to move one's hand. The most commonly used commands are best placed nearest to where a person's thumbs will be when holding a device, as indicated in the image below (from the Touch interaction design topic in the docs). Those spots are easier to reach (especially by those of us that can't grip a large ball with one hand!) and thus make the whole user experience more comfortable.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_460_0.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_460_1.png)

- The nav bar and app bar are always available in all views, regardless of size; in narrower views you can limit app bar commands to around 10 so that they can fit into one or two rows, and also omit labels and tighten up the hit targets. The WinJS app bar does this automatically.
- Know too that the app bar is not limited to circular command buttons: you can create whatever custom layout you like, which is how the nav bar is implemented. With any custom layout, make sure that your elements are appropriately sized for touch interaction. More on this—including a small graphic of the aforementioned finger of a basketball player—can again be found on Guidelines and checklist for app bars as well as Touch interaction design under “Touch targets.”

## Sidebar: Logins and License Agreements

As noted above, Microsoft recommends that login/account management and license agreements/terms-of-use pages are accessed through the Settings charm, where an app adds relevant commands to the Settings pane that first appears when the charm is invoked. These commands then invoke subsidiary pages with the necessary controls for each function. Of course, sometimes logins and license agreements need some special handling. For example, if your app requires a login or license agreement on startup, such controls can be shown on the app's first page, through the Web Authentication Broker (see Chapter 4, "Web Content and Services"), or in enterprise scenarios through the Credential Picker UI (see Appendix C, "Additional Networking Topics"). If the user provides a login and/or agrees to the terms of service, the app can continue to run. Otherwise, the app should show a page that indicates that a login or agreement is necessary to do something more interesting than stare at error messages.

If a login is recommended but not required, perhaps to enable additional features, you can place those controls directly on the canvas. When the user logs in, you can replace those controls with bits of profile information (user name and picture, for example, as on the Windows Start screen). If, on the other hand, a login is entirely optional, keep it within Settings.

In all cases, commands to view the license agreement, manage one's account or profile, and log in or out should still be available within Settings. Other app bar or on-canvas commands can invoke Settings programmatically, as we'll see in Chapter 10.

## The App Bar and Nav Bar

After placing essential commands on the app canvas, most of your app's commands will be placed in the app bar and navigation-specific commands in the top nav bar. Again, both bars are automatically brought up in response to various user gestures, such as a top or bottom edge swipe, Win+Z, or a right mouse button click. Whenever you perform one of these gestures, Windows looks for suitable controls on the current page and invokes them—you don't need to process any input events yourself. (Similarly, a click/tap outside the control or the ESC key dismisses them.)

**Tip** To prevent the app/nav bar from appearing, you can do one of two things. First, to prevent an app bar or nav bar from appearing at all (for any gesture), set the control's `disabled` property to true. Second, if you want to prevent it for, say, a right-click on a particular element (such as a canvas, listen to the `contextmenu` (right click) event for that element and call `eventArgs.preventDefault()` within your handler.

For apps written in HTML and JavaScript, the app bar control is implemented as a WinJS control, `WinJS.UI.AppBar`, and the nav bar with `WinJS.UI.NavBar`. As with all other WinJS controls, you declare either or both controls in HTML and instantiate them with a call to `WinJS.UI.process` or `WinJS.UI.processAll`. For a first example, we don't need to look any farther than some of the Visual Studio/Blend project templates like the Grid App project, where a placeholder app bar is included in default.html (initially commented out):

```html
<div id="appBar" data-win-control="WinJS.UI.AppBar">
    <button data-win-control="WinJS.UI.AppBarCommand"
        data-win-options="{id:'cmd', label:'Command', icon:'placeholder'}">
    </button>
</div>
```

The super-exciting result of this markup, using the ui-dark.css stylesheet, is as follows:

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_461_0.png)

Because the app bar is declared in default.html, which is the container for all other page controls, *this same app bar will apply to all the pages in the app*. With this approach you can declare all your commands within a single app bar and assign different classes to the commands that allow you to easily show and hide command sets as appropriate for each page. This also centralizes those commands that appear on multiple pages, and you can wire up event handlers for them in your app's primary activation code (such as that in default.js).
