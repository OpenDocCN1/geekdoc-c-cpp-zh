
**FIGURE 4.18** Done button with rounded corners

![](img/fe9fea534a8e7868f811f7cd33da015f_213_0.png)

Run the application again. Now when you press the unit button, our modal view’s Done button looks all fancy (Figure 4.18).

This works fine in portrait mode, but if you rotate the view, you’ll notice that our gradients don’t stretch to fill the button. The problem is, we cannot automatically resize these layers. Instead, we need to manually resize them whenever the system lays out our views. To do this, implement the view controller’s viewDidLayoutSubviews method.

```objective-c
- (void)viewDidLayoutSubviews {
    CALayer* layer = self.doneButton.layer;
    CGFloat width = layer.bounds.size.width;
    for (CALayer* sublayer in layer.sublayers) {
        if ([sublayer.name hasSuffix:@"Gradient"]) {
            CGRect frame = sublayer.frame;
            frame.size.width = width;
            sublayer.frame = frame;
        }
    }
}
```

This method is called right after the system lays out all our subviews. Here, we just grab a reference to our doneButton's layer and the layer's width. We then iterate over all the sublayers. If the sublayer has a name that ends with "Gradient," we resize it to match the button's width. This way our custom layers will be resized, but we won't alter any of the button's other layers.

Try it out. Switch back and forth between the enter weight and unit select views. Rotate the interface to all the different orientations. If everything is working, commit all our changes. Next stop, the history view.

## Core Animation and Performance

While we used the CALayer to give our button rounded corners, you could use the same technique for any UIView. One obvious example would be to create UIImageView objects with rounded corners and possibly even a glassy sheen. However, you may find it useful for any number of UIView objects: text views, Web views, scroll views, map views, or any of the custom views you may build.

While this approach is convenient, it can become computationally expensive. Performing these types of Core Animation manipulations require our views to be drawn to an offscreen buffer before being drawn onto the main view. This occurs on each and every frame both for our altered view and for any of its subviews.

This is particularly important in any view that expects smooth animation (for example, scroll views or table views). Having a number of objects performing offscreen rendering will quickly turn a smoothly scrolling interface into a jerking, stuttery mess.

We can use Instruments to detect views that are using offscreen rendering (see Bonus Chapter B for more information on Instruments). Connect your test iOS device, and set the scheme to run on it. Then select Product > Profile from the main menu. This will launch Instruments. When prompted, start the Core Animation template. Select the Core Animation track, and make sure the Color Offscreen-Rendered Yellow option is selected (Figure 4.19). This will highlight any views that are rendered offscreen in yellow, making them easy to spot.

As you can see, when you touch the units button, the entire screen is rendered offscreen as it flips. However, once the transition animation finishes, the rest can be rendered directly. Only our custom button continues to render offscreen (Figure 4.20).

If Core Animation becomes a performance issue, the easiest fix is to set the CALayer's shouldRasterize property to YES. This tells Core Animation that the layer will require offscreen rendering and will force it to cache the offscreen image and reuse it whenever possible. In some cases, this can dramatically improve Core Animation's performance.

However, shouldRasterize isn't a magic "run faster" flag. It should only be used under very specific circumstances. Obviously, if our view's appearance is changing, then caching doesn't make sense. Core Animation will need to throw out the cache and re-render the view for each new frame. Worse yet, if the view wouldn't have required an offscreen pass, setting shouldRasterize will force it to be rendered offscreen. This will actually reduce the app's performance.

In Health Beat, shouldRasterize doesn't help us at all. Our button's final image is only rendered once, so we would never reuse the cache. Creating it only wastes memory. However, if we had placed our button in a scroll view, setting shouldRasterize might make a big difference.

![](img/fe9fea534a8e7868f811f7cd33da015f_216_0.png)

**FIGURE 4.19** Highlighting offscreen-rendered views using Instruments

![](img/fe9fea534a8e7868f811f7cd33da015f_216_1.png)

**FIGURE 4.20** All offscreen-rendered views are highlighted in yellow

If we cannot use shouldRasterize to solve our performance problems, we may need to revert back to custom drawing. In our case, we could create a subclass of UIView and override the drawRect: method, manually drawing our curved rectangle and gradient fills. Typically, the drawing code is only called once, when the object is first placed onscreen. It is then cached in the view's CALayer and can be scrolled, resized, or otherwise animated without requiring additional drawing. Of course, the initial drawing may be slightly slower than the Core Animation method calls, but we're converting a per-frame cost into a one-time cost. In many cases, this produces significant performance improvements.

We'll cover custom drawing in more depth in Chapter 5, “Drawing Custom Views.”

## Showing Weight History

Now let’s shift over to our history view. Here, we display a list of all the entries in our WeightHistory. We will use a UITableView to present these entries, showing one entry per row. Let’s start by designing a custom cell for these rows.

Right-click the Views group and select New File > Objective-C Class. Make sure it is a subclass of UITableViewCell, and name it HistoryCell. Now open HistoryCell.h. Modify the header file as shown:

```objective-c
#import <UIKit/UIKit.h>
#import "WeightEntry.h"

@interface HistoryCell : UITableViewCell

@property (nonatomic, strong) IBOutlet UILabel* weightLabel;
@property (nonatomic, strong) IBOutlet UILabel* dateLabel;
- (void)configureWithWeightEntry:(WeightEntry*)entry
                     defaultUnits:(WeightUnit)unit;

@end
```

Unlike view controllers, outlets cannot be Control-dragged from the storyboard to a view’s header file. Instead, we need to manually declare them first. We’re also declaring a method to configure our cell—changing the contents of its labels based on the WeightEntry and WeightUnit arguments.

Switch to the implementation file. We’ll start by synthesizing our properties.

```objective-c
@synthesize weightLabel=_weightLabel;
@synthesize dateLabel=_dateLabel;
```

Then implement configureWithWeightEntry:defaultUnits:.

```objective-c
- (void)configureWithWeightEntry:(WeightEntry*)entry
                     defaultUnits:(WeightUnit)unit {
    self.weightLabel.text = [entry stringForWeightInUnit:unit];
    self.dateLabel.text =
        [NSDateFormatter
            localizedStringFromDate:entry.date
                         dateStyle:NSDateFormatterShortStyle
                         timeStyle:NSDateFormatterShortStyle];
}
```

Here, we use our WeightEntry’s stringForWeightInUnit: method to set the weightLabel outlet with a correctly formatted weight string. Next, we use NSDateFormatter to create a properly localized date string using the short date and short time formats. We then assign this to our dateLabel outlet.

Now, let’s open the storyboard and zoom in on our history view. Select the prototype cell and switch to the Identity inspector. Set the cell’s class to HistoryCell. Then switch back to the Attributes inspector. Make sure the Accessory attribute is set to Disclosure Indicator. This will add a gray chevron on the right side of our cell.

Xcode provides two built-in accessories with very similar functions. Both the Disclosure Indicator and the Detail Disclosure indicate that the application has additional information related to this row. However, there are slight differences, both in the way they operate and in their intended use.

Detail Disclosure creates a round blue button with a white chevron. When the user taps the button, it should navigate to a detail view for the selected item. The Disclosure Indicator, on the other hand, just provides the gray chevron image. Here, the user must select the row itself, and they are then navigated to a sublist (usually containing additional options).

Arguably, Health Beat should use Detail Disclosure accessories—but I feel that having users select the row, not the disclosure button, works better. Besides, our detail view is a list (of sorts), so it’s not wholly inappropriate, and even Apple isn’t 100 percent consistent with their accessories.

Now, drag out two labels. Set the first label’s title to Weight. Make it 100 points wide, and set the font to 18-pt System Bold. Then drag it until it is vertically centered along the cell’s left margin. In the Size inspector, lock its Autosizing position to the top and the left side.
