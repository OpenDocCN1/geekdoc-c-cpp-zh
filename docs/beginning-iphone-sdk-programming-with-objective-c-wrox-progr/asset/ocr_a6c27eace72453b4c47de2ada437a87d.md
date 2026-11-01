One important point to note here is that within the loadView method, you should not get the value of the view property (setting it is all right), like this:

```
[self.view addSubview: label];   //---this is not OK---
self.view = view;                //---this is OK---
```

Trying to get the value of the view property in this method will result in a circular reference and cause memory overflow.

# UNDERSTANDING VIEW HIERARCHY

As views are created and added, they are added to a tree data structure. Views are displayed in the order that they are added. To verify this, modify the location of the UIButton object you created earlier by changing its location to CGRectMake(10, 30, 300, 50), as in the following:

```
//---create a Button view---
frame = CGRectMake(10, 30, 300, 50);
UIButton *button = [UIButton buttonWithType:UIButtonTypeRoundedRect];
button.frame = frame;
[button setTitle:@"Click Me, Please!" forState:UIControlStateNormal];
button.backgroundColor = [UIColor clearColor];
button.tag = 2000;
[button addTarget:self action:@selector(buttonClicked:) forControlEvents:UIControlEventTouchUpInside];
```

When you now run the application again, you will notice that the button overlaps the label control (see Figure 4-19) since the button was added last:

```
[view addSubview:label];
[view addSubview:button];
```

![](bbox=[0.78, 0.6, 0.95, 0.83])

FIGURE 4-19

If you want to switch the order in which the views are displayed after they have been added, you can use the exchangeSubviewAtIndex:withSubviewAtIndex: method, like this:

```
[self.view addSubview:label];
[self.view addSubview:button];

[self.view exchangeSubviewAtIndex:1 withSubviewAtIndex:0];

[button release];
[label release];
```

The preceding statement in bold swaps the order of the Label and Button views. When the application is run again, the Label view will now appear on top of the Button view (See Figure 4-20).

![](bbox=[0.78, 0.8, 0.95, 0.97])

FIGURE 4-20