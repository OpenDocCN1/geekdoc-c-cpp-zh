

![](img/aab2d775c46f70cd606f2e58e2521324_352_0.png)

图 14-3

## 工作原理

前面的应用程序通过感应手指在 iPhone 或 iPod Touch 屏幕上的触摸来工作。当用户触摸屏幕时，视图（View）或视图控制器（View Controller）会触发一系列你可以处理的事件。共有四个此类事件：

- `touchesBegan:withEvent:`
- `touchesEnded:withEvent:`
- `touchesMoved:withEvent:`
- `touchesCancelled:withEvent:`

仔细看看第一个事件。首先，当在屏幕上检测到至少一次触摸时，会触发 `touchesBegan:withEvent:` 事件。在这个事件中，你可以通过调用 `UIEvent` 对象（event）的 `allTouches` 方法来知道屏幕上有多少根手指：

```
///---get all touches on the screen---
NSSet *allTouches = [event allTouches];
```

`allTouches` 方法返回一个 `NSSet` 对象，其中包含一组 `UITouch` 对象。要知道屏幕上有多少根手指，只需使用 count 方法计算 `NSSet` 对象中 `UITouch` 对象的数量。在这种情况下，你（此时）只对单个触摸感兴趣，因此你只实现了单次触摸的情况：

```
//---compare the number of touches on the screen---
switch ([allTouches count])
{
    //---single touch---
    case 1: {
        //---get info of the touch---
        UITouch *touch = [[allTouches allObjects] objectAtIndex:0];

        //---compare the touches---
        switch ([touch tapCount])
        {
            //---single tap---
            case 1: {
                imageView.contentMode = UIViewContentModeScaleAspectFit;
            } break;

            //---double tap---
            case 2: {
                imageView.contentMode = UIViewContentModeCenter;
            } break;
        }
    } break;
}
```

你可以使用 NSSet 对象的 allObjects 方法提取第一次触摸的详细信息，该方法返回一个 NSArray 对象。然后使用 objectAtIndex: 方法获取数组中的第一个项。

UITouch 对象（touch）包含 tapCount 属性，它告诉你用户是单击了屏幕还是进行了双击（或更多次）。如果用户单击了屏幕，你可以使用 UIViewContentModeScaleAspectFit 常量调整图像大小以完全适应整个 ImageView 视图。如果是双击，则使用 UIViewContentModeCenter 常量将其恢复到原始大小。

另外三个事件在本节中未讨论，它们是 touchesEnded:withEvent:、touchesMoved:withEvent: 和 touchesCancelled:withEvent:。

当用户的一根或多根手指从屏幕上抬起时，会触发 touchesEnded:withEvent: 事件。当用户的一根或多根手指在屏幕上触摸并移动时，会持续触发 touchesMoved:withEvent: 事件。最后，如果在用户手指仍在屏幕上时应用程序被中断，则会触发 touchesCancelled:withEvent: 事件。

> 注意 除了在 touchesBegan:withEvent: 事件中检测轻击外，你还可以在 touchesEnded:withEvent: 事件中检测它们。

## 理解多次轻击（Multi-Tapping）

当用户在屏幕上执行多次轻击时，你的应用程序会多次触发 `touchesBegan:` 和 `touchesEnded:` 事件。例如，如果用户点击屏幕一次，`touchesBegan:` 和 `touchesEnded:` 事件会被触发一次，`UITouch` 对象的 `tapCount` 属性返回值为 1。但是，如果用户（快速连续地）点击屏幕两次，那么 `touchesBegan:` 和 `touchesEnded:` 事件会被触发两次；第一次触发时，`tapCount` 属性为 1，第二次触发时，`tapCount` 属性为 2。

理解多次轻击的检测方式很重要，因为如果你正在检测双击，你的应用程序可能会冗余执行为单击设计的代码块。例如，在前面的动手练习中，双击图像会首先尝试将图像模式改为 `UIViewContentModeScaleAspectFit`（这是单击本应做的；在这种情况下，因为图像已经处于 `UIViewContentModeScaleAspectFit` 模式，用户不会注意到任何差异），然后改回 `UIViewContentModeCenter` 模式（这是双击本应做的）。理想情况下，它不需要执行单击的代码块。

要解决这个问题，你必须编写一些代码来检查第二次点击是否确实会到来：

- 当检测到单击时，使用一个 `NSTimer` 对象作为计时器。
- 当检测到双击时，停止计时器，并检查第二次点击与第一次点击之间的时间差是否小到足以构成双击（例如几分之一秒）。如果是，则执行双击的代码；否则，执行单击的代码。

在下一节中，你将学习如何在应用程序中检测多点触摸。

## 检测多点触摸（Multi-Touches）

在理解了上一节的概念之后，检测多点触摸其实非常简单。检测多点触摸的能力非常有用，因为你可以利用这种能力在应用程序中放大视图。

下面的动手练习将向你展示如何检测多点触摸。

## **动手练习** 检测多点触摸

1. 使用上一节中创建的同一个项目，修改 `touchesBegan:withEvent:` 方法，添加以下以粗体显示的语句：

```
```objc
- (void) touchesBegan: (NSSet *) touches withEvent: (UIEvent *) event {

    //---get all touches on the screen---
    NSSet *allTouches = [event allTouches];

    //---compare the number of touches on the screen---
    switch ([allTouches count])
    {
        //---single touch---
        case 1:
            //---get info of the touch---
            UITouch *touch = [[allTouches allObjects] objectAtIndex:0];

            //---compare the touches---
            switch ([touch tapCount])
            {
                //---single tap---
                case 1:
                    imageView.contentMode = UIViewContentModeScaleAspectFit;
                    break;

                case 2:
                    imageView.contentMode = UIViewContentModeCenter;
                    break;
            }
            break;

        //---double-touch---
        case 2 {
            //---get info of first touch---
            UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];

            //---get info of second touch---
            UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];

            //---get the points touched---
            CGPoint touch1PT = [touch1 locationInView:[self view]];
            CGPoint touch2PT = [touch2 locationInView:[self view]];

            NSLog(@"Touch1: %.0f, %.0f", touch1PT.x, touch1PT.y);
            NSLog(@"Touch2: %.0f, %.0f", touch2PT.x, touch2PT.y);
        }
    break;
    }
}
```
```

2. 按下 Command-R，在 iPhone 模拟器上测试应用程序。
3. 在 iPhone 模拟器中，按下 Option 键，应该会出现两个圆圈（见图 14-4）。点击屏幕可模拟两根手指触摸设备屏幕。点击并移动鼠标以模拟捏合屏幕。
4. 打开调试器控制台窗口（按 Command-Shift-R），并在 Option-点击 iPhone 模拟器屏幕时观察输出：

```
2009-08-25 10:01:15.510 MultiTouch[2230:207] Touch1: 107, 201
2009-08-25 10:01:15.511 MultiTouch[2230:207] Touch2: 213, 239
2009-08-25 10:01:15.758 MultiTouch[2230:207] Touch1: 105, 201
2009-08-25 10:01:15.759 MultiTouch[2230:207] Touch2: 215, 239
2009-08-25 10:01:15.918 MultiTouch[2230:207] Touch1: 215, 239
2009-08-25 10:01:15.919 MultiTouch[2230:207] Touch2: 105, 201
2009-08-25 10:01:16.054 MultiTouch[2230:207] Touch1: 105, 201
2009-08-25 10:01:16.055 MultiTouch[2230:207] Touch2: 215, 239
2009-08-25 10:01:16.238 MultiTouch[2230:207] Touch1: 105, 201
2009-08-25 10:01:16.239 MultiTouch[2230:207] Touch2: 215, 239
```

![](img/aab2d775c46f70cd606f2e58e2521324_356_0.png)

> 注意 使用 iPhone 模拟器时，当你 Option-点击 iPhone 模拟器屏幕上的同一点时，两个触摸的坐标经常会互换。

## 工作原理

与检测单次触摸时一样，你在 touchesBegan:withEvent: 事件中检查多点触摸。你现在不再只接收第一次触摸的信息，而是同时获取第一次和第二次触摸的信息：

```
//---get info of first touch---
UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];

//---get info of second touch---
UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];
```

> 注意 基本上，要检测两个以上的触摸，你只需扩展前面的代码，获取第三个触摸、第四个触摸等的信息。

