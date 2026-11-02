In the first case, an app that gets resumed will have all its previous data still in memory. It very much needs to decide, then, whether that data has become stale since the app was suspended and whether sessions with other servers have exceeded their timeout periods. You can also think of it this way: after what period of time will users not remember nor care what was happening the last time they saw your app? If it's a week or longer, it might be reasonable to resume or restart in a default state. Then again, if you pick up right back where they were, users gain increasing confidence that they can leave apps running for a long time and not lose anything. Or you can compromise and give the user options to choose from. You'll have to think through your scenarios, of course, but if there's any doubt, resume where the app left off.

To check elapsed time, save a timestamp on suspend (from new Date().getTime()), get another timestamp in the resuming event, take the difference, and compare that against your desired refresh period. A Stock app, for example, might have a very short period. With the Windows App Builder blog, on the other hand, new posts don't show up more than once per day, so a much longer period on the order of hours is sufficient to keep up-to-date and to catch new posts within a reasonable timeframe.

This is implemented in SimpleXhr2 by first placing the getStringAsync call into a separate function called downloadPosts, which is called on startup. Then we register for the resuming event with WinRT:

```
```javascript
WinJS.UI.WinRT.WebUIApplication.onresuming = function () {
    app.queueEvent({ type: "resuming" });
};
```
```

Remember how I said in Chapter 3, "App Anatomy and Performance Fundamentals," we could use WinJS.Application.queueEvent to raise our own events to the app object? Here's a great example. WinJS.Application doesn't automatically wrap the resuming event because it has nothing to add to that process. But the code above accomplishes exactly the same thing, allowing us to register an event listener right alongside other events like checkpoint.

```
```javascript
app.oncheckpoint = function (args) {
    //Save in sessionState in case we want to use it with caching
    app.sessionState.suspendTime = new Date().getTime();
};

app.addEventListener("resuming", function (args) {
    //This is a typical shortcut to either get a variable value or a default
    var suspendTime = app.sessionState.suspendTime || 0;

    //Determine how much time has elapsed in seconds
    var elapsed = ((new Date().getTime()) - suspendTime) / 1000;

    //Refresh the feed if > 1 hour (or use a small number for testing)
    if (elapsed > 3600) {
        downloadPosts();
    }
});
```
```

To test this code, run it in Visual Studio's debugger and set breakpoints within these events. Then click the suspend button in the toolbar, and you should enter the checkpoint handler. Wait a few