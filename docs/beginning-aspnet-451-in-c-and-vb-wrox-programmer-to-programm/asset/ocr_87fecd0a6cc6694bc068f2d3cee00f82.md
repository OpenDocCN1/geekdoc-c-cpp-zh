(VerticalPanel) and calls slideToggle, which hides in the matched set when they are visible and show them when they aren't. If the check uses the css method on the VerticalPanel element (now referred to with this keyword) and asks for its display property. When it is block it means the banner and the text must be Hide Banner. Otherwise, the text is set to Show Banner. Finally, you need to hide the link when the banner is in horizontal mode in the banner's Code Behand:

# VB.NET

```
Case Direction.Horizontal
HorizontalPanel.Visible = True
VerticalPanel.Visible = False
HorizontalLink.HRef = NavigateUrl
HideBanner.Visible = False
```

# C#

```
case Direction.Horizontal:
HorizontalPanel.Visible = true;
VerticalPanel.Visible = false;
HorizontalLink.HRef = NavigateUrl;
HideBanner.Visible = false;
break;
```

# Exercise 2 Solution

The slideUp method hides elements by slowly decreasing its height. slideDown shows hidden elements by doing the reverse: slowly increasing the height of an element until it's fully visible. Both methods accept, among others, a speed parameter that either accepts a fixed value (slow, normal, or fast) or a number specifying the speed of the animation in milliseconds.

# Exercise 3 Solution

jQuery document ready functions fires when the page is loading in the browser, during the initial request. The pageLoad method fires both when the page loads first and after an asynchronous postback, for example, using an UpdatePanel. This difference enables you to choose the desired behavior. Need to fire some code on initial load and after a postback? Choose pageLoad. Otherwise, use document ready function.

# Exercise 4 Solution

You use the _references.js file in the Scripts folder to enable IntelliSense. VS will read this file and all JavaScript files that you added with this syntax:

```
/// <reference path="Path/To/File.js" />
```

This way, you get IntelliSense in files where it would not be supported (such as user controls) or for JavaScript files that you're not directly linking to your website.