
**Note** I’m using an `iframe` element in this first example because it’s probably familiar to most readers. In Chapter 4, “Web Content and Services,” we’ll change the app to use an `x-ms-webview` element, which is much more flexible than an `iframe` and is the recommended means to host web content.

I’ve also included various `aria-*` attributes on these elements (as the templates do) that support accessibility. We’ll look at accessibility in detail in Chapter 19, “Apps for Everyone, Part 1,” but it’s an important consideration that we should be conscious of it from the start: a majority of Windows users make use of accessibility features in some way. And although some aspects of accessibility are easy to add later on, adding `aria-*` attributes in markup is best done early.

In Chapter 19 we’ll also see how to separate strings (including ARIA labels) from our markup, JavaScript, and even the manifest, and place them in a resource file for the purposes of localization. This is something you might want to do from early on, so see the “Preparing for Localization” section in that chapter for the details. Note, however, that resource lookup doesn’t work in Blend, so you might want to hold off on the effort until you’ve done most of your styling.

## Styling in Blend

At this point, and assuming you were paying enough attention to read the footnotes, Blend’s real-time display of the app shows an obvious need for styling, just like raw markup should. See Figure 2-10.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_59_0.png)

**FIGURE 2-10** The app in Blend without styling, showing a view that is much like the Visual Studio simulator. If the taphere.png image doesn’t show after adding it, use the View/Refresh menu command.

The tabs along the upper left give you access to your Project files, Assets like all the controls you can add to your UI, and a browser for all the Style Rules defined in the environment. On the lower left side, the Live DOM tab lets you browse your element hierarchy and the Device tab lets you set orientation, screen resolution, view sizes and positions, and minimum size. Clicking an element in the Live DOM will highlight it in the designer, and clicking an element in the designer will highlight it in the Live DOM section. Also note the search bar in the Live DOM, where you can enter any CSS selector to highlight those elements that match that selector.

Over on the right side you see what will become a very good friend: the section for HTML Attributes and CSS Properties. With properties, the list at the top shows all the sources for styles that are being applied to the currently selected element and where, exactly, those styles are coming from (often a headache with CSS). The location selected in this list, mind you, indicates where changes in the properties pane below will be written, so be very conscious of your selection! That list also contains an item called “Winning Styles,” which shows the styles that are actually being applied to the element, and an item called “Computed Values,” which will show you the exact values applied in the layout engine, such as the actual sizes of rows and columns in a CSS grid and how values like 1.5em translate into pixels.

Now to get our gauche, unstylish page to look like the wireframe, we need to go through the elements and create the necessary selectors and styles. First, I recommend creating a 1x1 grid in the body element as this seems to help everything in the app size itself properly. So add `display: -ms-grid; -ms-grid-rows: 1fr; -ms-grid-columns: 1fr;` to `default.css` for `body`.

- Set the insertion point of the style rule within Blend’s Style Rules tab by dragging the orange-yellow line control. This determines exactly where any new rule you create will be written. In the image below, new rules would be inserted in `default.css` at the beginning of the `landscape/max-width: 1024px` media query:

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_60_0.png)

- In the Live DOM pane (the lower left side in Blend, where you can again search for rules to highlight elements that use them), right-click the element you want to style and select Create Style Rule From Element Id or Create Style Rule From Element Class. This will create a new style rule (at the insertion point indicated in Style Rules above). Then in the CSS properties pane on the right, find the rule that was created and add the necessary style properties.

**Note** If the menu items in the Live DOM pane are both disabled, go to the HTML Attributes pane (upper right) and add an id, a class, or both, then return to the menu in the Live DOM. If you do styling without having a distinct rule in place, you’ll create inline styles in the HTML, although Blend makes it easy to copy those out and paste them into a rule.

- Repeat with every other element you want to style, which could include `body`, `html`, and so forth, all of which appear in the Live DOM.

So for the *mainContent* div, we create a rule from the Id and set it up with `display: -ms-grid; -ms-grid-columns: 1fr; -ms-grid-rows: 140px 1fr 60px;`. (See Figure 2-11) This creates the basic vertical areas for the wireframes. In general, you won’t want to put left or right margins directly in this grid because the lower section will often have horizontally scrolling content that should bleed off the left and right edges. In the case of *Here I Am!* we could use one grid, but instead we’ll add those margins in a nested grid within the `header` and `section` elements.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_61_0.png)

**FIGURE 2-11** Setting the grid properties for the *mainContent* div. Notice how the View Set Properties Only checkbox (upper right) makes it easy to see what styles are set for the current rule. Also notice how the grid rows and columns appear on the artboard, including sliders (circled) to manipulate rows and columns directly.

Showing this and the rest of the styling—going down into each level of the markup and creating appropriate styles in the appropriate media queries—is best done in video. Video 2-2 shows this process starting with the creation of the project, styling the different views, and switching to Visual Studio (right-click the project name in Blend and select Edit In Visual Studio) to run the app in the simulator for verification. It also demonstrates the approximate time it takes to style such an app once you're familiar with the tools. (I also highly recommend watching What's New in Blend for HTML Developers from //build 2013, which goes much more in depth with various styling processes.)

The result of all this in the simulator looks just like the wireframes—see Figures 2-12 through 2-14—and all the styling is entirely contained within the appropriate media queries of default.css. Most importantly, the way Blend shows us the results in real time is an enormous time-saver over fiddling with the CSS and running the app over and over again, a painful process that I'm sure you're familiar with! (And the time savings are even greater with Interactive Mode; see Video 5-3 and the //build 2013 talk linked above.)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_62_0.png)

FIGURE 2-12 Full landscape view.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_63_0.png)

**FIGURE 2-13** Partial landscape view (when sharing the screen with other apps).

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_63_1.png)

**FIGURE 2-14** Narrow aspect ratio views: 320px wide (left), 50% wide (middle), and full portrait (right). These images are not to scale with one another. You can also see that the fixed placeholder image in the Photo section doesn't scale well to the 50% view; we'll solve this later in this chapter in "Improving the Placeholder Image with a Canvas Element."

## Adding the Code

Let's complete the implementation now in Visual Studio. Again, right-click the project name in Blend's Project tab and select Edit In Visual Studio if you haven't already. Note that if your project is already loaded into Visual Studio when you switch to it, it will (by default) prompt you to reload changed files. Say yes. At this point, we have the layout and styles for all the necessary views, and our code doesn't need to care about any of it except to make some refinements, as we'll see.

What this means is that, for the most part, we can just write our app's code against the markup and not against the markup plus styling, which is, of course, a best practice with HTML/CSS in general. Here are the features that we'll now implement:

- A Bing maps control in the Location section showing the user's current location. We'll create and display this map automatically.
- Use the WinRT APIs for camera capture to get a photograph in response to a tap on the Photo img element.
- Provide the photograph and the location data to the Share charm when the user invokes it.

Figure 2-15 shows what the app will look like when we're done, with the Share charm invoked and a suitable target app like Twitter selected.

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_64_0.png)

FIGURE 2-15 The completed Here I Am! app with the Share charm invoked (with my exact coordinates blurred out, because they do a pretty accurate job of pinpointing my house).
