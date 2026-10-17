FIGURE 17.30 The Schemes pop-up with some new run destinations

![](bbox=[0.28, 0.15, 0.76, 0.26])

If you take a look at the Schemes pop-up, you'll see at least two new run destinations (for the iPhone and iPad Simulators) for TestApp Touch (Figure 17.30). One simulates the iPhone and the other simulates the iPad. If you've already connected and provisioned any iOS devices (see Appendix A), those will show up as individual run destinations as well.

# QUITTING APPLICATIONS

It may seem odd that there needs to be a section about quitting applications. The reason is that many new iOS developers become confused when they press the Home button on the device or Simulator but the application continues running in Xcode. This is because of how iOS handles applications when the Home button is pressed.

Applications in the most recent versions of iOS can be paused in the background (unless they opt out of this functionality). This means the application is still technically running, it's just suspended. Unless your application opts out of being “backgrounded,” it won’t quit (and won’t end the Xcode debugging session) when you press the Home button.

There are two ways to quit an iOS application completely when you're debugging it: Press Command+Q in the Simulator to quit the entire iOS Simulator, or click the Stop button in Xcode's toolbar.