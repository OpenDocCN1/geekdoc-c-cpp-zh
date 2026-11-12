![](bbox=[0.07, 0.145, 0.73, 0.535])

**FIGURE 3.18** Connecting a segue from the cell prototype

Right-click our history view controller’s prototype cell. Draw a connection from its Push storyboard segue to our detail view controller (**Figure 3.18**). That’s it. As long as we create all our history view’s table cells using that prototype, they will automatically launch the detail view when selected.

You may also notice that interface builder automatically adds the navigation bar to all the views linked to our navigation controller. However, these bars look a little bit plain. Let’s add custom titles to them. In our history view controller scene, double-click the navigation bar and set its title to **History** (alternatively, select the navigation bar and set the Title attribute). Do the same for the detail view controller, but set the title to **Weight Entry**.

That’s it. Take a few seconds to zoom out and organize your storyboard. When you’re done, it should look like **Figure 3.19**.

Let’s take our new user interface out for a spin. Unfortunately, there are a few loose threads we need to tie off before it will compile. Zoom in on our history view controller again, and select its prototype cell. We need to set the cell’s reuse identifier. We’ll discuss reuse identifiers in detail in the “Showing Weight History” section of Chapter 4. For now, open the Attributes inspector, and set the Identity attribute to **History Cell**.