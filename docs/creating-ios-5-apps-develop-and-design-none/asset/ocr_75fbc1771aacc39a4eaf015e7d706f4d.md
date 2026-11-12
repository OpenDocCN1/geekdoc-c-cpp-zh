We only have one segue, so we know the identifier will always match. However, checking the identifier helps future-proof our code. We won’t suddenly have odd bugs just because we added a new segue.

Also, if you remember, the showAlternate segue connects our main view controller scene with our flipside view controller scene. This means the destination ViewController will be our HWFlipsideViewController.

So, the user presses the info button, triggering our segue. The system instantiates a copy of our HWFlipsideViewController, then calls the HWMainViewController’s prepareForSegue:sender:. Here, HWMainViewController assigns itself as HWFlipsideViewController’s delegate. The transition occurs, and our view flips over horizontally, revealing the flipside view. When the flipside view is finished (which we will see in a minute), the flipside view controller calls flipsideViewControllerDidFinish: on its delegate, HWMainViewController. HWMainViewController then dismisses the flipside view controller and our views flip back over, revealing the main view again.

It’s important to realize that this pattern demonstrates the preferred technique for passing data from scene to scene across a segue. When passing data from the originating view controller to the destination view controller, we override the originating view controller’s prepareForSegue:sender: method and pass the data along. To pass the data back, we make the originating view a delegate of the destination view and then call the appropriate delegate methods. Of course, these methods need to be declared in the delegate’s protocol. We’ll see the HWFlipsideViewControllerDelegate’s protocol next.

Open HWFlipsideViewController.h. Here, we start by declaring our HWFlipsideViewControllerDelegate protocol. This only has a single method, which we have already seen, flipsideViewControllerDidFinish:. Next, we declare the HWFlipsideViewController class itself. This is also simple, containing only two items: the delegate outlet property and the done: action.

We’ve seen both of these before. We just discussed the delegate property in relationship to our HWMainViewController, and we saw the done: action back when we were exploring our storyboard. It is connected to the Done button in the navigation bar. Pressing that button will trigger this method.

```
```objc
#import <UIKit/UIKit.h>

@class HWFlipsideViewController;

@protocol HWFlipsideViewControllerDelegate
```
```