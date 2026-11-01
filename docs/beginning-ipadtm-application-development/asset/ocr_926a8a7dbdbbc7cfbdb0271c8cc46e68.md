```
return NO;
}
-(void) dealloc {
    [textField release];
    [scrollView release];
    [super dealloc];
}
```

10. Save the project in Xcode and press Command-R to deploy the application onto the iPhone Simulator. Figure 5-18 shows that when you click the TextField view, the keyboard appears and the TextField view (along with other views) is scrolled to the center of the screen. To hide the keyboard, simply click the Return key, and the views are restored to their original positions.

![](bbox=[0.07, 0.33, 0.72, 0.95])

FIGURE 5-18