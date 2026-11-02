```
```html
<div class="section3" data-win-control="WinJS.UI.HubSection"
    data-win-options="{header: 'Video', isHeaderStatic: true}">
    <video class="promoVideo" src="images/cycle.mp4" controls></video>
</div>
<!-- section4 omitted -->
</div>
```
```

**Tip** Do you see the select('.pagecontrol').winControl.myData.dataSource reference for the ListView's itemDataSource property in section 2? The pageControl class identifies the myData property defined within the page control element defined in html/basichub.js. That element's winControl property gets you to the object defined with WinJS.UI.Pages.define, wherein you'll find the myData property that returns a Binding.List.

The item template for the ListView is, of course, defined earlier in html/basichub.html. Styles are pulled in from pages/commonstyles.css, which we'll look at in the next section after we finish up with the other Hub control features.

Scenario 2 of the sample now adds a hero image at the beginning of the Hub, the full result of which is shown in Figure 8-11 and the limited 1366x768 view in Figure 8-12. In reality, the hero image is not actually a concept of the Hub control at all—it's simply another HubSection that's been added to the top of the list (pages/heroimage.html).

```
```html
<div data-win-control="WinJS.UI.Hub">
    <div class="hero" data-win-control="WinJS.UI.HubSection"
        data-win-options="{header: 'Hero'}"></div>
    <div class="section1" data-win-control="WinJS.UI.HubSection"
        data-win-options="{header: 'Images', isHeaderStatic: true}">
```
```

where the styling for the `hero` class in pages/heroimage.css sets the image, the width, and margins, and hides the section header (using the `win-hub-section-header` selector):

```
```css
.hero {
    background-image: url(/images/circle_hero.jpg);
    background-size: cover;
}

.win-hub-horizontal .hero {
    width: 944px;
    margin-left: -80px;
    margin-right: 80px;
}

.win-hub-section.hero .win-hub-section-header {
    visibility: hidden;
}
```
```

No magic here—just straight CSS, although it's important to note that the HubSection control extends fully top to bottom within the Hub, so the background image bleeds to the edges.