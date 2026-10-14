off, but here’s how to do this as of the time of this writing.

First, enter chrome://settings/passwords into the Address Bar of Chrome. Then turn off the following:

![](bbox=[0.146, 0.128, 0.853, 0.235])

If this isn’t at this location in Chrome when you try, I’d suggest doing a Google search for how to turn it off.

And realize that if you do this, it’ll turn off asking to remember passwords for ALL websites, so you may want to turn it back on later.

Also, keep in mind that this error is benign, although annoying.

# 30.10. ChangePassword Page

We’re going to make the ChangePassword Page just have a button on it that we’ll click and it’ll redirect us to the Users page since we don’t have an API for setting a permenant password.

We should fomulate a plan for coding this.

First, we’ll use the code from the Logon Page as a template.

Second, we’ll start with defining:

+   - Input (from Parent)
+   - Output (to Parent)
+   - State
+   - Action (events from EventListeners)
+   - Query (H.tell or H.request from Parent)
+   - Slots (for Children)

Then write:

+   - component
+   - handleAction (for the button click)
+   - render (put the button in the center of the screen using Flex Grid)

If you don’t already know how to center a button in a div using display flex using align-items and justify-content, then take the time know to Google it. I’d suggest using the MDN (Mozilla Developer Network) link that shows up.