
Finally, we check the document’s `UIDocumentStateEditingDisabled` flag. This is set whenever the document is in a state where editing the document is no longer safe. Typically, this happens when the document is loading a remote update, but other events may trigger it as well.

If the flag is turned on, we have our text field resign first responder status, hiding the keyboard. We also disable the text field, preventing the user from making any changes. If the flag is turned off, we enable the text field and set it as the first responder. This causes the keyboard to reappear. We also update our `currentDate` property and the user interface’s date label. This helps ensure that our weight entries remain in sequential order.

That wraps up our work with the document; however, we still need to save the user defaults. Fortunately, as you will see, this is much, much easier. Still, this is a good place to take a break. Stretch for a bit, and (as always) commit your changes.

## SAVING USER DEFAULTS

We’re going to start by storing the default weight units using `NSUserDefaults`. First, let’s define a few functions to simplify our code.

We are just going to write C functions, but we still want them to have full access to our Objective-C classes. So, we need the file to be compiled as if it were Objective-C. The easiest way to do this is to create a new NSObject class and then delete both the class interface and its implementation.

Right-click the Model group and create a new NSObject named WeightUnits. Then open up both the header and implementation file and delete everything except the `#import` directives. We can even move the Foundation import directive from the header to the implementation file.

Now, in WeightUnits.h, add the following code:

```objc
typedef enum {

    LBS,

    KG

} WeightUnit;

WeightUnit getDefaultUnits(void);

void setDefaultUnits(WeightUnit value);
```

Here we’re just defining our `WeightUnit` enum and declaring two accessor functions for our default weights.

Next, switch to the implementation file.

```objc
#import "WeightUnits.h"

#import <Foundation/Foundation.h>

static NSString* const WeightUnitKey = @"weight_unit";

WeightUnit getDefaultUnits(void) {
    return [[NSUserDefaults standardUserDefaults]
        integerForKey:WeightUnitKey];
}

void setDefaultUnits(WeightUnit value) {
    [[NSUserDefaults standardUserDefaults]
        setInteger:value forKey:WeightUnitKey];
}
```

`NSUserDefaults` stores values using keys, so we start by defining a static string to use as our key. The `getDefaultUnits()` function simply accesses the standard user defaults and returns the value associated with our key. `setDefaultUnits()` saves a new value into the standard user defaults, also using our key.

We will be using these functions in several places throughout our application. So, let’s add an `#import` directive to our precompiled prefix header file. Open Health Beat-Prefix.pch and modify it as shown.

![](img/fe9fea534a8e7868f811f7cd33da015f_360_0.png)

```objc
#import <Availability.h>

#ifndef __IPHONE_5_0

#warning "This project uses features only available in iOS SDK 5.0
        and later."

#endif

#ifdef __OBJC__

    #import <UIKit/UIKit.h>

    #import <Foundation/Foundation.h>

    #import "WeightUnits.h"

#endif
```

This automatically imports `WeightUnits.h` into every class in our project, making our accessor functions available everywhere.

Now we need to go through our project and replace every instance of `self.weightHistory.defaultUnits` with one of our two accessor functions. To start, switch to the Search navigator (the icon that looks like a magnifying glass in the navigator selector bar) and perform a search for `self.weightHistory.defaultUnits` (Figure 6.6).

Our search has found seven matches. Select each one in turn. If the code is getting the default unit value, replace it with a call to `getDefaultUnits()`.

```objc
WeightUnit unit = getDefaultUnits();
```

If the matching code is setting a new default unit value, replace it with a call to `setDefaultUnits()`.

```objc
setDefaultUnits(unit);
```

We also need to delete the `WeightUnit` typedef from the top of WeightEntry.h. We've already copied it over to WeightUnits.h, and having a duplicate will just cause compilation errors.

Finally, we need to update our UI whenever our default units change. Fortunately, `NSUserDefaults` posts an `NSUserDefaultsDidChangeNotification` whenever its values change. We just need to listen for this notification.

In EnterWeightViewController.m, navigate to the `viewDidLoad` method and add the following code to the bottom of the method.

```objc
    [[NSNotificationCenter defaultCenter]
    addObserverForName:NSUserDefaultsDidChangeNotification
    object:[NSUserDefaults standardUserDefaults]
    queue:nil
    usingBlock:^(NSNotification *note) {
        NSString* title = [WeightEntry stringForUnit:
            getDefaultUnits()];
        [self.unitsButton setTitle:title
            forState:UIControlStateNormal];
    }];
```

Then, in the `viewDidUnload` method, we need to unregister ourselves.

```objc
    [[NSNotificationCenter defaultCenter]
    removeObserver:self];
```

In GraphViewController's `viewDidLoad` method, register for a similar notification. Remember to unregister in the `viewDidUnload` method as well.

```objc
    // Register to receive notifications when the default unit changes.
    [[NSNotificationCenter defaultCenter]
    addObserverForName:NSUserDefaultsDidChangeNotification
    object:[NSUserDefaults standardUserDefaults]
    queue:nil
    usingBlock:^(NSNotification *note) {
        [graphView
            setWeightEntries:self.weightHistory.weights
            andUnits:getDefaultUnits()];
    }];
```

We also want to register our HistoryViewController for notifications as well. Again, add the following to its `viewDidLoad` method. As always, remember to unregister in the `viewDidUnload` method.

```objc
// Register to receive notifications when the user
// defaults change.
    [[NSNotificationCenter defaultCenter]
      addObserver:self
      selector:@selector(reloadTableData)
      name:NSUserDefaultsDidChangeNotification
      object:[NSUserDefaults standardUserDefaults]];
```

Finally, we want to make sure our EnterWeightController view starts with the correct units. Open EnterWeightViewController.m and navigate to the `viewWillAppear:` method. Add the following code.

```objc
- (void)viewWillAppear:(BOOL)animated {
    // Sets the current time and date.
    self.currentDate = [NSDate date];
    self.dateLabel.text =
      [NSDateFormatter
        localizedStringFromDate:self.currentDate
        dateStyle:NSDateFormatterLongStyle
        timeStyle:NSDateFormatterShortStyle];
    // Clear the text field.
    self.weightTextField.text = @"";
    [self.weightTextField becomeFirstResponder];
    [self.unitsButton
      setTitle:[WeightEntry stringForUnit:getDefaultUnits()]
      forState:UIControlStateNormal];
    [super viewWillAppear:animated];
}
```

The project should now build without any errors. Try running it. Add a few weights. Change the default units. Now send the app to the background, and then stop it. Run it again. It should remember both the weight entries and the changed units.

> **NOTE:** Sending the app to the background forces the application to save any pending changes. On the other hand, pressing the Stop button in Xcode will immediately kill the app without giving it a chance to save its state. When testing any document-based project, it’s always best to send the app to the background before stopping it.

![](img/fe9fea534a8e7868f811f7cd33da015f_363_0.png)

Try running the app on two devices. Add a new weight to one device, and then send the app to the background. You should see the new entry show up on the second device within about 30 seconds.

Try adding a new weight to both simultaneously. Send both apps to the background, and then bring them back to the foreground. Both apps should initially appear with their own unique set of weights. Then one app will resolve the conflict, changing to display the merged set of weights. A minute or so later, the other app will also change over. The conflict is now resolved.

Note that both copies of our app are successfully syncing their weight history, but they’re not syncing the default units. Let’s fix that.

## IMPLEMENTING iCLOUD KEY-VALUE STORAGE

We want to continue to use `NSUserDefaults` to store our preferences locally; however, we can use iCloud key-value storage to sync these defaults between machines. The procedure is simple. We register for notifications about changes to our iCloud key-value storage. If a change occurs, we modify our user defaults to match. Similarly, we monitor our user defaults. If they change, we update the iCloud key-value storage. Furthermore, we can do all of this in our application delegate. Our view controllers already respond to any changes we make to our user defaults.
