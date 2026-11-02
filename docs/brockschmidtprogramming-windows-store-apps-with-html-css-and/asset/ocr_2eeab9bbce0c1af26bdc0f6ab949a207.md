```
win-appbar.customFont {
  font-family: "Wingdings";
}
```

To change the font of a specific command button, add a class to its extraClass property (such as customButtonFont) and create a rule with the following selector (as used in scenario 1 of the modified sample that will show if you add extraClass: 'otherFont' to a button):

```
button.otherFont .win-commandimage {
  font-family: "Wingdings";
}
```

To provide graphics of your own, do the following for a 100% resolution scale:

+   - Create a 160x80 pixel png sprite image with a transparent background, saving the file with the .scale-100 suffix in the filename.
+   - This sprite is divided into two rows of four columns—that is, 40x40 pixel cells. The top row is for the light styling theme, and the bottom is for the dark theme.
+   - Each row has four icons for the following button states, in this order from left to right: default (rest), hover, pressed (active), and disabled.
+   - Each image is centered in its respective 40x40 cell, but remember that a ring will be drawn around the icon, so generally keep the image in the 20-30 pixel range vertically and horizontally. It can be wider or taller in the middle areas, of course, where the ring is widest.

For other resolution scales, multiple the sizes by 1.4 (140%) and 1.8 (180%) and use the .scale-140 and .scale-180 suffixes in the image filename.

To use the custom icon, point the command's icon property to the base image URI (without the .scale-1x0 suffixes)—for instance, icon: 'url(images/icon.png)' .

Scenario 3 of the HTML Appbar Control sample demonstrates custom icon graphics for an Accept button:

![](bbox=[0.15, 0.7, 0.35, 0.88])

The icon comes from a file called accept.png, which appears something like this—I’ve adjusted the brightness and contrast and added a border so that you can see each cell clearly: