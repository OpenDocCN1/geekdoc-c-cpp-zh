![](bbox=[0.06, 0.18, 0.7, 0.45])

![](bbox=[0.73, 0.15, 0.94, 0.32])

**FIGURE 4.4** Autorotation works, but autosizing does not.

**FIGURE 4.5** Locking the control to the top of the view

However, if you run the app you may notice that autorotation still isn't working. No matter how you twist the device, the interface remains locked in the portrait orientation.

That's because there's a trick. By default, tab views only allow autorotation if all of the contained view controllers support autorotation. Make the same change to the `HistoryViewController` and the `GraphViewController`, and then run the app again.

And...it's still not working. OK, I lied. There were two tricks. When we created a custom tab view, it turns out that we inadvertently overrode the tab bar's default `shouldAutorotateToInterfaceOrientation:` implementation. Open `TabBarController.m`, and delete the `shouldAutorotateToInterfaceOrientation:` method. This will restore the default behavior. Run it one last time. It should finally rotate as expected. Unfortunately, we have another problem (Figure 4.4). The UI elements are not properly resizing or repositioning themselves in the new, wider view.

To fix this, open `MainStoryboard.storyboard` again. Select the Enter Today's Weight label, and open the Size inspector. The Autosizing control allows us to lock the object's position relative to the top, bottom, left, or right sides. It also allows us to automatically stretch and shrink our control horizontally or vertically.

By default, the view is locked to the left and top. We want it locked to the top—but we want it to remain centered in the view. Click the red I-bar on the left side of the Autosizing control to turn it off. After you make changes in the Autosizing control, check the Example preview to make sure the control will behave as you expect. In this case, it should remain centered at the top of the view as the size changes (Figure 4.5).