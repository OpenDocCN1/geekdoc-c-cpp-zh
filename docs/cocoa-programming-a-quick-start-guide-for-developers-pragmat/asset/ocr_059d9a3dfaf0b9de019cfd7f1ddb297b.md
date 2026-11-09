Take a minute to look at how little code we need when we work *with* the existing Apple frameworks. Whenever your code gets long and complicated, you should pause and consider whether there’s an easier way to accomplish what you are trying to do. Your goal is to write simple code that is clear and understandable. Cocoa programmers do not value code that is short and clever to the point of being obscure.

# ## 9.12 Exercise: Adding a Progress Indicator

A lot of what we’re doing at this point is adding muscle memory as we jump back and forth between Xcode and Interface Builder. Let’s take this example one step further—at least on the desktop.

Add a small circular progress indicator to the top-right side of your browser. It should be initially hidden. When a user enters a new URL or navigates to a different page, the progress indicator should appear and start to spin. We want to give the user some feedback that something is happening. Once the page has fully loaded, the progress indicator should stop spinning and should be hidden again.

Think through the steps. You need to place a progress indicator using IB. You need to add an outlet for that indicator in the BrowserController header file and then connect it in IB. You need to synthesize the property you just created and use it when the page starts and stops loading.

# ## 9.13 Solution: Adding a Progress Indicator

You can look at the solution provided in the code download to investigate the nib and header file. Here’s the Attributes inspector settings for the progress indicator:

![](bbox=[0.32, 0.863, 0.593, 0.989])