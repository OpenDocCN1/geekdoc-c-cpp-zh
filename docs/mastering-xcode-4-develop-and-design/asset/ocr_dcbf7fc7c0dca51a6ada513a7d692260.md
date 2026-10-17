Next, you’ll add a simple class whose only mission in life is to answer its -description method with a simple “Hello World!” Repeat the New File process, selecting the Objective-C Class template from the Cocoa category. When you click Next, supply the class name NSObject for the “Subclass of” field. Click Next again to be prompted to save. Change the filename in the Save As field to TestFoo, and click Save. Make sure the TestFoo.m source file is selected in the Project navigator so that its source is visible in the editor. Just above the @end directive at the end of the file, add the following method:

```
- (NSString *)description
{
    return @"Hello World!";
}
```

This gives the TestFoo class the ability to say hello when asked for its description. You’ll use that later. For now, you need to add its header file, TestFoo.h, to the framework’s umbrella header for later import. Navigate to TestAppSharedFramework.h in the Project navigator and add the following on a new line at the end of the file:

```
#import "TestFoo.h"
```

Any other classes you add to your framework can be similiarly included in this umbrella header. This way, when your framework is used, there is only one header to import, which brings the headers of any other classes along for the ride. Try a build (Command+B) and verify there are no build issues. The framework should build cleanly.