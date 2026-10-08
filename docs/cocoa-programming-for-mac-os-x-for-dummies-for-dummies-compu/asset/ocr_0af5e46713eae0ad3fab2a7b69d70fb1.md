4. Connect the new action to the interface.

Control+drag from the new button in your interface to the MyPrintController instance in the XIB project window. Select printToPDF from the small black connections list overlay that appears.

5. Return to Xcode and add the new printToPDF action to the MyPrintController.h file:

```
/* MyPrintController */

#import <Cocoa/Cocoa.h>

@interface MyPrintController : NSObject
{
IBOutlet id myCanvasView;
NSPrintInfo *thePrintInfo;
}

- (IBAction)printOnePage:(id) sender;
- (IBAction)showPagePanel:(id) sender;
- (IBAction)printToPDF:(id) sender;
@end
```

6. Add the following code to implement the printToPDF method in the MyPrintController.m file:

```
- (IBAction)printToPDF:(id) sender
{
NSRect theRect;
NSData *theData;

theRect = [myCanvasView bounds];
theData = [myCanvasView dataWithPDFInsideRect:
theRect];
[theData
writeToFile: [@"~/Desktop/MyView.pdf"
stringByExpandingTildeInPath]
atomically: YES];
}
```

Just to keep matters simple, this method creates a PDF file on the desktop.

1. The code starts by getting the bounds of the NSRect that surrounds the view.

2. With those bounds, dataWithPDFInsideRect provides you with raw PDF data for use in a file.