# Figure 16.18

With the filter running, the sharp lines of the Bezier paths are replaced with wispy blurs. The Radius parameter controls the amount of blur. This is the output of a single filter, but you can combine filters almost indefinitely to create sophisticated multiple effects.

![](bbox=[0.186, 0.239, 0.603, 0.524])

Figure 16.19 shows the application’s nib and UI. The Filter Browser View and the Filter View are both subclasses of NSView. The Browser View manages the interface. It responds to mouseDown: events within the application window and implements two sliders that are linked to two filter parameters. This view exists to manage the UI, and its drawRect: method isn’t used.

The Filter View receives its settings from the UI, and implements the filter. A filter object is created with a call to CIFilter using the filterWithName: method:

```
CIFilter *thisFilter =
    [CIFilter filterWithName: @"CITwirlDistortion"];
```

CIFilter parameters are accessed through key value coding:

```
[thisFilter setValue: [NSNumber numberWithFloat: 50]
           forKey: @"inputRadius"];
```