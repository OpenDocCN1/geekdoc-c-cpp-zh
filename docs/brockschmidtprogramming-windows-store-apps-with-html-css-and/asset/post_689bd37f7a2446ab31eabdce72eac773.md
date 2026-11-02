
```
args.setPromise(winJS.UI.processAll());
}
};
app.oncheckpoint = function (args) {
};
app.start();
})();
```

We'll come back to checkpoint in Chapter 3. For now, remember from Chapter 1, “The Life Story of a Windows Store App,” that an app can be activated in many ways. These are indicated in the args.detail.kind property whose value comes from the Windows.ApplicationModel.Activation.ActivationKind enumeration.

When an app is launched directly from its tile on the Start screen (or in the debugger as we’ve been doing), the kind is just launch. As we’ll see later on, other values tell us when an app is activated to service requests like the search or share contracts, file-type associations, file pickers, protocols, and more. For the launch kind, another bit of information from the Windows.ApplicationModel.Activation.ApplicationExecutionState enumeration tells the app how it was last running. Again, we’ll see more on this in Chapter 3, so the comments in the default code above should satisfy your curiosity for the time being.

Now, what is that args.setPromise(winJS.UI.processAll()) for? As we’ll see many times, WinJS.UI.processAll instantiates any WinJS controls that are declared in your HTML—that is, any element (commonly a div or span) that contains a data-win-control attribute whose value is the name of a constructor function. The Blank app template doesn’t include any such controls, but because just about every app based on this template will, it makes sense to include it by default.10 As for args.setPromise, that’s employing something called a deferral that we’ll also defer to Chapter 3.

As short as it is, that little app.start(); at the bottom is also very important. It makes sure that various events that are queued during startup get processed. We’ll again see the details in Chapter 3. I’ll bet you’re looking forward to that chapter now!

Finally, you may be asking, “What on earth is all that ceremonial (function () { ... })(); business about?” It’s just a convention in JavaScript called a self-executing anonymous function that implements the module pattern. This keeps the global namespace from becoming polluted, thereby propitiating the performance gods. The syntax defines an anonymous function that’s immediately executed, which creates a function scope for everything inside it. So variables like app along with all the function names are accessible throughout the module but don’t appear in the global namespace.11

10 There is a similar function winJS.Binding.processAll that processes data-win-bind attributes (Chapter 6), and winJS.Resources.processAll that does resource lookup on data-win-res attributes (Chapter 19).

11 See Chapter 2 of Nicolas Zakas’s High Performance JavaScript (O’Reilly, 2010) for the performance implications of scoping. More on modules can be found in Chapter 5 of JavaScript Patterns by Stoyan Stefanov (O’Reilly, 2010) and Chapter 7 of Eloquent JavaScript by Marijn Haverbeke (No Starch Press, 2011).

You can still introduce variables into the global namespace, of course, and to keep it all organized, WinJS offers a means to define your own namespaces and classes (see WinJS.Namespace.define and WinJS.Class.define), again helping to minimize additions to the global namespace. We'll learn more of these in Chapter 5, "Controls and Control Styling," and Appendix B, "WinJS Extras."

Now that we've seen the basic structure of an app, let's build something more functional and get a taste of the WinRT APIs and a few other platform features.

**Get familiar with Visual Studio** If you're new to Visual Studio, the tool can be somewhat daunting at first because it supports many features, even in the Express edition. For a quick, roughly 10-minute introduction, Video 2-1 (reminder: also available with this preview's companion content) will show you the basic workflows and other essentials.

## QuickStart #1: Here My Am! and an Introduction to Blend for Visual Studio

When my son was three years old, he never—despite the fact that he was born to two engineer parents and two engineer grandfathers—peeked around corners or appeared in a room saying "Hello world!" No, his particular phrase was "Here my am!" Using that variation of announcing oneself to the universe, our next app can capture an image from a camera, locate your position on a map, and share that information through the Windows Share charm. Does this sound complicated? Fortunately, the WinRT APIs actually make it quite straightforward!

### Sidebar: How Long Did It Take to Write This App?

This app took me about three hours to write. "Oh sure," you're to which user actions. Chapter 14, "Purposeful Animations," discusses the different built-in animations that you can use for this purpose.

When I had the idea for this app, I drew up simple wireframes, let a few designers laugh at me behind my back (and offer helpful adjustments), and eventually landed on layouts for the various views as shown in Figures 2-7 through 2-9. These reflect the guidelines of the "grid system" described on [Laying out an app page](...), which defines what's called the layout *silhouette* that includes the size of header fonts, their placement, and specific margins. These recommendations encourage a degree of consistency between apps so that users' eyes literally develop muscle memory for common elements of the UI. That said, they are not hard and fast rules—designers can and do depart from when it makes sense.

Generally speaking, layout is based on a basic 20 pixel unit, with 5 pixel sub-units. In the full landscape view of Figure 2-7, you can see the recommended left margin of 120px, the recommended top margin of 140px above the content region, and placement of the header's baseline at 100px, which for a 42pt font translates to a 44px top margin. For partial landscape views with width <= 1024px, the left margin shrinks to 40px (not shown). In the portrait and narrow views of Figure 2-8 and 2-9, the various margins and gaps get smaller but still align to the grid.
