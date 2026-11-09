Make the corresponding changes to the method signatures in the implementation file:

```
```objective-c
-(IBAction) loadIconView:(id) sender {
    self.ac = [[IconViewController alloc]
               initWithNibName:@"IconView" bundle:nil];
    [self setUpView];
}
```
```

```
```objective-c
-(IBAction) loadTableView: (id) sender {
    self.ac = [[ActivityController alloc]
               initWithNibName:@"ActivityView" bundle:nil];
    [self setUpView];
}
```
```

You’ll also need to add self as a parameter when you call these methods from inside initWithWindowNibName:

```
```objective-c
if ([self shouldLoadIconView]) [self loadIconView:self];
else [self loadTableView:self];
```
```

Save your work, and open MainMenu.xib in Interface Builder. Use the Connections inspector to connect these actions to their corresponding menu items. Save.

Click Build & Run, and you should be able to toggle back and forth between the two views using the menu items or the keyboard equivalents. Every time we toggle back to the Icon view, it displays the launch notification for HelloApplication. The problem is in the setUpView method.

```
```objective-c
-(void) setUpView {
    self.currentApp = [[CurrentApp alloc] init];
    self.currentApp.delegate = self.ac;
    [self.window setContentSize:[self.ac.view bounds].size];
    self.window.center = self.ac.view;
    [self.ac applicationDidLaunch:
                  [NSRunningApplication currentApplication]];
}
```
```

The setUpView method was meant to be called only once when the application first launches. Now it is called every time we switch views. There’s no reason to create a fresh instance of CurrentApp every time we switch views. We also only want to hard-code the fact that we are launching the current application the first time through.