```
```objc
        [NSString stringWithFormat:@"%i", theCount];
    }
    - (IBAction) flipButtons: (id) sender {
        if (upButton.action == @selector(addOne)) {
            upButton.action = @selector(subtractOne);
            [upButton setContinuous: NO];
            upButton.title = @"Down";
            downButton.action = @selector(addOne);
            [downButton setContinuous: NO];
            downButton.title = @"Up";
        } else {
            upButton.action = @selector(addOne);
            [upButton setContinuous: YES];
            upButton.title = @"Up";
            downButton.action = @selector(subtractOne);
            [downButton setContinuous: YES];
            downButton.title = @"Down";
        }
    }
    @end
```
```

# Other applications of selectors

Table 9.1 lists some other ways that selectors and target-action are used in Cocoa.

**Table 9.1** Selected Advanced applications of target-action and selectors

| Application | Description |
|---|---|
| NSTimer | Supports both target and action. Selects a method that is called on each timer tick or after a delay. |
| performSelector: | A method built into NSObject and supported by most classes. Supports both target and action. Selects a method that can be run immediately or after a delay. Supports explicit multithreading. |
| performSelectorInBackground: | A very simple way to run a method in a separate background thread. |
| Data collection objects: NSArray and so on | Include a makeObjectsPerformSelector: method that automatically enumerates through every object in the collection and runs the selected method on it. |
| Core Animation | Certain Core Animation classes can trigger a selector when an animation completes. Use this for composite multiple animations or to control user input while the animation runs. |
| NSInvocation | Wraps a selector and a target into a combined object with parameters to create a powerful composite. Sometimes used to manage Cocoa's undo system. |
| canPerformSelector: | A method that can be run on any object to check whether it implements a selector. Use it to avoid crashes and error messages. |