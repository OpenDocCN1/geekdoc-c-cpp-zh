# Your First iPhone Application

463

![](bbox=[0.218, 0.114, 0.781, 0.368])

```
// iPhone_AppDelegate.h
// @interface
// Created by Steve Kanan on 1/20/11.
// Copyright 2011 DFT Software. All rights reserved.

#import <UIKit/UIKit.h>

@interface iPhone_AppDelegate : NSObject

@property (nonatomic, retain) UIWindow *window;
@property (nonatomic, retain) UILabel *label;
-(void)IBAction:(id)sender;

@end
```

Figure 21.14 Displaying source code alongside the interface.

![](bbox=[0.218, 0.476, 0.781, 0.73])

```
// iPhone_AppDelegate.h
// @interface
// Created by Steve Kanan on 1/20/11.
// Copyright 2011 DFT Software. All rights reserved.

#import <UIKit/UIKit.h>

@interface iPhone_AppDelegate : NSObject

@property (nonatomic, retain) UIWindow *window;
@property (nonatomic, retain) UILabel *label;
-(void)IBAction:(id)sender;

@end
```

Figure 21.15 Adding an action for a button.