```
```css
#createNavBar .win-navbar {
  border-top: 10px solid #008299;
}
```
```

Within the NavBar, any of your own child elements (like the TRAVEL and FEATURED labels in the Travel app) have whatever classes you assign to them. If you have NavBarContainer elements, those are composed of a considerable hierarchy of parts:

![](bbox=[0.13, 0.21, 0.89, 0.47])

To color the page indicators like the Travel app, for example, uses these rules:

```
```css
#createNavBar .win-navbarcontainer-pageindicator {
  background-color: #636363;
}

#createNavBar .win-navbarcontainer-pageindicator-current {
  background-color: #008299;
}
```
```

The viewport and pageindicator-box (if I may drop the win-navbarcontainer- prefix) are sibling elements, each of which has its own portion within the container where you can style background colors, margins/padding, etc.

Within the viewport we then have the pannable surface area alongside the left and right navigation arrows. The navarrow style specifically styles the arrow inside the buttons; the navleft and navright selectors (including pseudo-styles) affect the surrounding controls.

Within the win-navbarcontainer-surface element is where you’ll find the NavBarCommand elements, each of which has this hierarchy of elements and classes, through which you can specifically address whichever part you want: