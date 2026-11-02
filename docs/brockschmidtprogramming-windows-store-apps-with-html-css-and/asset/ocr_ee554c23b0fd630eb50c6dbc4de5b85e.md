![](bbox=[0.141, 0.083, 0.446, 0.209])

The declaration for the app bar button then appears as follows (some properties omitted for brevity):

```
```html
<button data-win-control="WinJS.UI.AppBarCommand"
    data-win-options="{'id':'cmdAccept', 'label':'Accept', 'icon':'url(images/accept.png)'}">
```
```

Note that although the sample doesn’t have variations of the icon for resolution scales, it does provide variants for high contrast themes, an important accessibility consideration that we’ll come back to in Chapter 19. For this reason, the `button` element includes `style="-ms-high-contrast-adjust:none"` to override automatic adjustments for high contrast.

# Command Menus

The next aspect of an app bar we need to explore in a little more depth are those commands whose `type` property is set to `flyout`. In this case the command’s `flyout` property must identify a `WinJS.UI.Flyout` object or a `WinJS.UI.Menu` control (which is a flyout). As noted before, flyout or popup menus like this are used when there are too many related commands cluttering up the basic app bar, or when you need other types of controls that aren’t quite appropriate on the app bar itself. It’s said, though, that if you’re tempted to use a button labeled “More”, “Advanced”, or “Other Stuff” because you can’t figure out how to organize the commands otherwise, it’s a good sign that the app itself is too complex! Seek ways to simplify the app’s purpose so that the app bar doesn’t just become a repository for randomness.

We’ll be covering flyouts more fully a little later in this chapter, but let’s see how to use one in an app bar, as demonstrated in scenario 6 of the [HTML flyout control sample](#) (not the app bar sample, mind you!):

![](bbox=[0.158, 0.716, 0.331, 0.89])