
The hooks for this are a property called ready (a promise) and two methods, loadImage and isOnScreen, that are attached to the item provided by the itemPromise:

```javascript
renderComplete: itemPromise.then(function (item) {
    // item.ready, item.loadImage, and item.isOnScreen available
})
```

Here's how you use them:

- **ready** Return this promise from the first completed handler in any async chain you might use in the renderer. This promise is fulfilled when the full structure of the element has been rendered and is visible. This means you can chain another then with a completed handler in which you do post-visibility work like loading images.
- **isOnScreen** Returns a promise whose fulfillment value is a Boolean indicating whether the item is visible or not. In present implementations, this is a known value, so the promise is fulfilled synchronously. By wrapping it in a promise, though, it can be used in a longer chain.
- **loadImage** Downloads an image from a URI and displays it in the given img element, returning a promise that's fulfilled with that same element. You attach a completed handler to this promise, which itself returns the promise from isOnScreen. Note that loadImage will create an img element if one isn't provided and deliver it to your completed handler.

The following code shows how these are used (where element.querySelector traverses only a small bit of the DOM, so it's not a concern):

```javascript
renderComplete: itemPromise.then(function (item) {
    // mutate the element to update only the title
    if (!label) { label = element.querySelector(".content"); }
    label.innerText = item.data.title;

    // use the item.ready promise to delay the more expensive work
    return item.ready;
    // use the ability to chain promises, to enable work to be cancelled
}).then(function (item) {
    //use the image loader to queue the loading of the image
    if (!img) { img = element.querySelector("img"); }
    return item.loadImage(item.data.thumbnail, img).then(function () {
        //once loaded check if the item is visible
        return item.isOnScreen();
    });
}).then(function (onscreen) {
    if (!onscreen) {
        //if the item is not visible, then don't animate its opacity
        img.style.opacity = 1;
    } else {
        //if the item is visible then animate the opacity of the image
        WinJS.UI.Animation.fadeIn(img);
    }
})
```

I warned you that there would be promises aplenty in these performance optimizations! But all we have here is the basic structure of chained promises. The first async operation in the renderer updates simple parts of the item element, such as text. It then returns the promise in item.ready. When that promise is fulfilled—or, more accurately, if that promise is fulfilled—you can use the item's async loadImage method to kick off an image download, returning the item.isOnScreen promise from that completed handler. When and if that isOnScreen promise is fulfilled, you can perform those operations that are relevant only to a visible item.

I again emphasize the if part of all this because it's very likely that the user will be panning around within the ListView while all this is happening. Having all these promises chained together makes it possible for the ListView to cancel the async operations any time these items are scrolled out of view and/or off any buffered pages. Suffice it to say that the ListView control has gone through a lot of performance testing!

Which brings us to the final multistage batching renderer, which combines the insertion of images in the DOM to minimize layout and repaint work. It does this by letting loadImage create the img elements for us, so they're not initially in the DOM, and then inserting batches of them until there's a 64-millisecond gap between images coming in.

The sample does this inside a renderComplete that now has this structure (most code omitted):

```javascript
renderComplete: itemPromise.then(function () {
  item = i;
  // ...
  return item.ready;
}).then(function () {
  return item.loadImage(item.data.thumbnail);
}).then(thumbnailBatch()
).then(function (newimg) {
  img = newimg;
  element.insertBefore(img, element.firstElementChild);
  return item.isOnScreen();
}).then(function (onscreen) {
  //...
})
```

This is almost the same as the multistage renderer except for the insertion of a call to this mysterious thumbnailBatch function between the item.loadImage call and the item.isOnScreen check. The placement of thumbnailBatch() in the chain indicates that its return value is a completed handler that itself returns another promise, and somewhere in there it takes care of the batching.

The thumbnailBatch function itself is created by another function called createBatch, which is one of the finest examples of promise magic you'll see:

```javascript
//During initialization (outside the renderer)
thumbnailBatch = createBatch();

//The implementation of createBatch
function createBatch(waitPeriod) {
  var batchTimeout = WinJS.Promise.as();
  var batchedItems = [];

  function completeBatch() {
      var callbacks = batchedItems;
      batchedItems = [];

      for (var i = 0; i < callbacks.length; i++) {
          callbacks[i]();
      }
  }

  return function () {
      batchTimeout.cancel();
      batchTimeout = WinJS.Promise.timeout(waitPeriod || 64).then(completeBatch);

      var delayedPromise = new WinJS.Promise(function (c) {
          batchedItems.push(c);
      });
      return function (v) { return delayedPromise.then(function () { return v; }); };
  };
}
```

This code is designed to be something you can just drop into your own apps with complete blind faith that it will work as advertised; you don't have to understand (or even pretend to understand) how it works. Still, I know some readers will be curious, so I've deconstructed it all at the end of Appendix A, “Demystifying Promises.”

## What We’ve Just Learned

- The `WinJS.UI.Repeater` provides a simple and lightweight means to iterate over a `Binding.List` and render a data-bound template for each item into a container.
- The `WinJS.UI.FlipView` control displays one item of a collection at a time; `WinJS.UI.ListView` displays multiple items according to a specific layout. Both support different options, different behaviors, and rich styling capabilities.
- Central to all collection controls is the idea that there is a data source and an item template used to render each item in that source. Templates can be either declarative or procedural.
- ListView works with the added notion of layout. WinJS provides three built-in layouts. `GridLayout` is a two-dimensional, horizontally or vertically panning list; `CellSpanningLayout` is a horizontal `GridLayout` that allows items to span rows or columns; `ListLayout` is for a one-dimensional vertically or horizontally panning list. It is also possible to implement custom layouts.
- ListView provides the capability to display items in groups, organizing items into groups according to a group data source. `WinJS.Binding.List` provides methods to create grouped, sorted, and filtered projections of items from a data source.

## Chapter 8

## Layout and Views

Compared to other members of my family, I seem to need the least amount of sleep and am often up late at night or up before dawn. To avoid waking the others, I generally avoid turning on lights and just move about in the darkness (and here in the rural Sierra Nevada foothills, it can get *really* dark). Yet because I know the layout of the house and the furniture, I don’t need to see much. I only need a few reference points like a door frame, a corner on the walls, or the edge of the bed to know exactly where I am. What’s more, my body has developed a muscle memory for where doorknobs are located, how many stairs there are, how many steps it takes to get around the bed, and so on. It’s really helped me understand how visually impaired people “see” their own world.

If you observe your own movements in your home and your workplace—probably when the spaces are lit—you’ll probably find that you move in fairly regular patterns. This is actually one of the most important considerations in home design: a skilled architect looks carefully at how people in the home might move between primary spaces like the kitchen, dining room, and living room, and even within a single workspace like the kitchen. Then they design the home's layout so that the most common patterns of movement are easy and free from obstructions. If you’ve ever lived in a home where it *wasn’t* designed this way, you can very much appreciate what I’m talking about!

There are two key points here: first, good layout makes a huge difference in the usability of any space, and second, human beings quickly form habits around how they move about within a space, habits that hopefully make their movement more efficient and productive.

Good app design clearly follows the same principles, which is exactly why Microsoft recommends following consistent patterns with your apps, as described on the [Design Principles](#) page and [UX Patterns](#). Those recommendations are not in any way whimsical or haphazard: they are the result of many years of research and investigation into what would really work best for apps and for Windows as a whole. The placement of the charms, for instance, as well as commands on an app bar (as we'll see in Chapter 9, “Commanding UI”), arise from the reality of human anatomy, namely how far we can move our thumbs around the edges of the screen when holding a tablet device.

With page layout, in particular, the recommendations on [Laying out an app page](#)—about where headers and body content are ideally placed, the spacing between items, and so forth—can seem rather limiting, if not draconian. The silhouette, however, is meant to be a good starting point, not a hard-and-fast rule. What’s most important is that the shape of an app’s layout helps users develop a visual and physical muscle memory that can be applied across many apps. Research has shown that users will actually develop such habits very quickly, even within a matter of minutes, but of course those habits are not exact to specific pixels! In other words, the silhouette represents a general shape that helps users immediately understand how an app works and where to go for certain functions, just like you can easily recognize the letter “S” in many different fonts. This is very efficient and productive.
