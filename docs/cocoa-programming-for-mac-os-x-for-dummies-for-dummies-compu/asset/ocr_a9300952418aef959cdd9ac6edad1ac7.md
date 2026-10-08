The window in Figure 9-18 displays each type of NSIndicator.

# Figure 9-18:

The indefinite NSIndicator looks like a barber pole or spin in a circle. The determinate NSIndicator shows the progress of an operation, step by step.

![](bbox=[0.22, 0.18, 0.58, 0.42])

To use the indeterminate NSIndicator control, call the startAnimation method. This causes the barber pole to move. The following example calls the startAnimation method using an indeterminateProgress outlet from within an action:

```
- (IBAction)startIndeterminateProgress:(id)sender {
	[theIndeterminateProgress startAnimation:sender];
}
```

When you've finished processing whatever you need to process, you can stop the animation by using the stopAnimation method:

```
- (IBAction)stopIndeterminateProgress:(id)sender {
	[theIndeterminateProgress stopAnimation:sender];
}
```

With a determinate NSIndicator, you set the value of the control with the setDoubleValue: method. This code snippet sets the indicator to the middle position, assuming that the control has a minimum and maximum of 0 to 100, respectively:

```
[theDeterminateProgress setMinValue: 0.0];
[theDeterminateProgress setMaxValue: 100.0];
[theDeterminateProgress setDoubleValue: 50.0];
```