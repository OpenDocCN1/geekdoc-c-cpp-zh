
Besides defining MyPrintController as an NSObject, the only other addition is this line:

```objc
NSPrintInfo *thePrintInfo;
```

This line declares a pointer to an NSPrintInfo object as an instance variable to help you store settings that the user makes in the Page and Print panels.

## 7. Select the MyPrintController.m file and change its code to read

```objc
#import "MyPrintController.h"

@implementation MyPrintController

- (IBAction) showPagePanel:(id) sender {
	int i;
	thePrintInfo = [NSPrintInfo sharedPrintInfo];
	NSPageLayout *pageLayout = [NSPageLayout
		pageLayout];
	i = [pageLayout runModalWithPrintInfo: (NSPrintInfo *)thePrintInfo];
}

@end
```

Here’s how the code works:

- 1. The showPagePanel method first populates the thePrintInfo variable with the NSPrintInfo value, which is shared by all applications.
- 2. The code creates an NSPageLayout instance and displays it using the runModalWithPrintInfo method.

By passing thePrintInfo to the runModalWithPrintInfo method, the Page panel retains its settings in thePrintInfo when the user dismisses it.

So far, this code is functional but not terribly interesting. You can run it and choose File→Page Setup to view and play with the settings in the Page panel.

## Setting Up the Print Job and Printing the View

To add printing, all you have to do is implement the printOnePage action that you defined as part of MyPrintController in the preceding section. Click the MyPrintController.m file in Xcode and change its code to read

```objc
#import "MyPrintController.h"

@implementation MyPrintController

- (IBAction)showPagePanel:(id)sender {
    int i;
    thePrintInfo = [NSPrintInfo sharedPrintInfo];
    NSPageLayout *pageLayout = [NSPageLayout pageLayout];
    i = [pageLayout
         runModalWithPrintInfo:(NSPrintInfo *)
             thePrintInfo];
}

- (IBAction)printOnePage:(id)sender
{
    thePrintInfo = [NSPrintInfo sharedPrintInfo];
    NSPrintOperation *thePrintOperation;

    thePrintOperation =
        [NSPrintOperation printOperationWithView:
         myCanvasView printInfo:thePrintInfo];

    [thePrintOperation setShowPanels: YES];
    [thePrintOperation runOperation];
}

@end
```

The printOnePage method takes care of running the Print panel and executing the print job in this way:

- 1. It creates an NSPrintOperation instance using the class method printOperationWithView.
- 2. You pass the printOperationWithView method a view to print and an NSPrintInfo instance.
- 3. The `printOperationWithView` method returns an instance of `NSPrintOperation`.
- 4. (Optional but typical in most applications) If you want to display the Print panel, call the `setShowPanels`, passing it a Boolean value of YES.
- 5. The `runOperation` method of the `NSPrintOperation` object runs the print job.

Cocoa takes care of everything else for you, including dismissing the Print panel and printing the view.

## Printing to Places Other Than a Printer

So far, you’ve implemented some pretty boring stuff. Printing is nice, but it’s become a standard requirement on all applications and operating systems and it’s not altogether exciting. When it comes to printing, Cocoa really shines in its capability to print directly to PDF (Portable Document Format) files. Instead of printing your view to a standard printer, you can ask Cocoa to save it to a PDF-formatted file instead. PDF is a standard format for publishing and printing documents. In the past, you had to rely on third-party solutions when creating PDF content on the fly. With Cocoa, it’s as easy as adding a few lines of code to your project.

Before you begin adding PDF features to your project, you should know that you already have one form of PDF printing: The user can click the PDF button that’s at the bottom of the Print panel.

Here’s a more elegant solution if you don’t like that users have to open the Print panel to print to PDF:

- 1. Open the MainMenu.xib file in the project for this chapter.
- 2. Add a new push button to the existing interface by dragging one from the Library window.

Figure 14-6 shows what the interface looks like.

![](img/ea40cad434a338535474e82c1a6ace20_295_0.png)

Figure 14-6: Add a new button that users click to print to a PDF file.

- 3. Add a new action to the MyPrintController class.

Click MyPrintController in the XIB project window, press ⇧+6 to open the Identity Inspector window, and add a new printToPDF action, as shown in Figure 14-7.

![](img/ea40cad434a338535474e82c1a6ace20_295_1.png)

Figure 14-7: Add a new printToPDF action to the MyPrint Controller class.

![](img/ea40cad434a338535474e82c1a6ace20_295_2.png)

- 4. Connect the new action to the interface.

Control+drag from the new button in your interface to the MyPrintController instance in the XIB project window. Select printToPDF from the small black connections list overlay that appears.

- 5. Return to Xcode and add the new printToPDF action to the MyPrintController.h file:

```objc
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

- 6. Add the following code to implement the printToPDF method in the MyPrintController.m file:

```objc
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
3. The `writeToFile` method saves the data to a file.

You can view the resulting PDF with popular PDF viewers, such as the Apple Preview application, the Adobe Acrobat Reader, or a Web browser like Safari.

![](img/ea40cad434a338535474e82c1a6ace20_297_0.png)

Although this method doesn't exactly use printing classes, you can always print from your project with the Print panel. For this reason, PDF is part of the printing chapter.

# Chapter 15

## Cocoa on the Internet

**In This Chapter**

- Loading a Web site with Cocoa
- Downloading files from the Internet
- Sending e-mails with only a few lines of code

The last two decades of personal computing have witnessed explosive growth in networking technologies. Consequently, the vast majority of personal computer owners use the Internet, many on a daily basis. Among the various means of communication available to a user on the Internet, the World Wide Web and e-mail stand out as the two main tools that everyone uses.

In this chapter, you explore the wild and wooly world of the Internet and see how it applies to Cocoa applications. The chapter starts by showing you how to load Web pages, download files, and render HTML (HyperText Markup Language) in your own projects. Later, you add e-mail features to your application as well. By the end of this chapter, you’ll have a fully functional project that performs some important Internet functions. Although it’s not necessarily the kind of application you’ll want to use for your next best-selling killer app, it can serve as a handy reference for future projects.

## Interacting with the Web

Just over a decade ago, few were familiar with the Internet or the World Wide Web. Now, even your dog has a domain name, an e-mail address, and a MySpace account. Computer users have eaten up all that the Internet has to offer and in the process have become discerning consumers. They expect instant connectivity to any Web site in the world. Luckily, Cocoa has you covered. Perhaps the two most popular tasks on the Web are viewing Web pages and downloading files. With only a few lines of code, Cocoa gives you the ability to offer these important Internet functions in your own applications.
