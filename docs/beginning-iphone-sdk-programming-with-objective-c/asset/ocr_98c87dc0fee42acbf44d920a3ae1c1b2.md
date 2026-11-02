method is not defined in this controller; instead, it must be defined by whatever calls it (in this case, it is the MainViewController). Its use is to signal to the calling view controller that it is done and control should return to the calling view controller.

> NOTE Appendix C discusses protocols in more detail.

In the FlipsideViewController.m file, the implementation for the done: method is defined in the header file:

```
- (IBAction)done {
    [self.delegate flipsideViewControllerDidFinish:self];
}
```

Basically this method calls the flipsideViewControllerDidFinish: method that you have defined (but implemented elsewhere) in the FlipsideViewControllerDelegate protocol.

Now, double-click the FlipsideView.xib file to open it in Interface Builder. Observe the following:

+   - The Flipside view contains a Navigation Bar view and a Bar Button view (see Figure 9-4).
+   - The done: action is connected to the Done button. (Right-click the File's Owner item to view its connected actions and outlets.)

![](bbox=[0.08, 0.7, 0.85, 0.9])

FIGURE 9-4