Now, kill the server with Ctrl-C and run it again with:

```
make run
```

When I do this and refresh my browser page, I get 0 on the page. If you don’t then make sure you’re doing a Hard Reload on Chrome with Shift-Cmd-R on Mac or Ctrl-F5 on Windows. Don’t forget this won’t work if the Developer Tools are not currently visible.

Now, that we see the 0, we know our component is working.

Now, open up your Console in the Developer Tools. In Chrome, hit F12 in Mac or Windows or Cmd-Option-J on the Mac.

When I do this, I can see that Initialized is printed on the Console. This happens when the Initialize Action is performed.

At the moment, there’s no easy way for us to test Finalize, so we’ll leave that for later.

Let’s revisit our diagram and mark off what we’ve accomplished: