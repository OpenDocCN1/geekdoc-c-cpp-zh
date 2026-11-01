3. In the MyViewController.m file, define the btnClicked: action as follows:

```
```objc
-(IBAction) btnClicked:(id) sender{
    //---remove the current view; essentially hiding the view---
    [self.view removeFromSuperview];
}
```
```

4. Double-click the MyView.xib file to edit it in Interface Builder.

Control-click and drag the OK button in the View window to the File's Owner item in the MyView.xib window and select btnClicked:.

5. Back in Xcode, press Command-R to test the application. When you now click the OK button in the main View, you are brought to the second View (see Figure 7-15). To close the second View, press the OK button.

![](bbox=[0.12, 0.38, 0.68, 0.7])

FIGURE 7-15

# How It Works

For this example, you simply add the View of the view controller (that you are switching to) to the current view using the addSubview: method:

```
```objc
//---add the view of the view controller to the current View---
myViewController = [[MyViewController alloc]
    initWithNibName:@"MyView" bundle:nil];
[self.view addSubview:myViewController.view];
```
```

To dismiss a view, you use the removeFromSuperview: method:

```
```objc
//---remove the current view; essentially hiding the view---
[self.view removeFromSuperview];
```
```