![](bbox=[0.2, 0.13, 0.8, 0.55])

FIGURE 2-12

> NOTE Only one application can run on the iPad at any time (except for some built-in applications by Apple). Hence, when you press the Home button on your iPad, your application exits. Tapping an application icon starts the application all over again.

# Changing Screen Orientations

The iPad Simulator also supports changes in view orientation. To change the view orientation mode, press the Command→ or Command← key combination. Figure 2-13 shows the iPhone Simulator in Portrait mode.

Notice that your application automatically flips upright when you change the orientation mode. This is controlled programmatically in one of the code files in your Xcode project.

In Xcode, edit the HelloWorldViewController.m file and look for the following code segment:

```
// Override to allow orientations other than the default portrait orientation.
- (BOOL)shouldAutorotateToInterfaceOrientation:(UIInterfaceOrientation)
interfaceOrientation {
    return YES;
}
```