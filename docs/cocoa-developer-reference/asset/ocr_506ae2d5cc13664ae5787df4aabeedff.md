```
//This is the handler block
if (result == NSFileHandlingPanelOKButton) {
    //Save the file on OK, do nothing on Cancel
    [theTextView.string writeToURL: savePanel.URL atomically: YES
    encoding: NSUTF8StringEncoding error:nil];
}
}; //This is the end of the handler
}];

- (void) openADocument: (id) sender {
    NSOpenPanel *openPanel = [NSOpenPanel openPanel];
    openPanel.allowedFileTypes = [NSArray arrayWithObject:@"txt"];
    [openPanel beginSheetModalForWindow:self
    completionHandler:^(NSInteger result) {

        if (result == NSFileHandlingPanelOKButton) {
            // If OK, load the file
            NSString *theText = [NSString stringWithContentsOfURL:openPanel.URL encoding: NSUTF8StringEncoding error:nil];
            [theTextView setString: theText];
        }
    }];
}
```

# Key points of the code:

+   1. The first line creates a save panel and initializes it with an array that preselects `.txt` files.
+   2. The second line displays the sheet. It runs modally, locking out the rest of the application.
+   3. The result handler is inside a block. It checks the return button status and does nothing if the user cancelled. Otherwise, it writes the data to a file as a string, at the URL returned from the pane.
+   4. The open method is almost identical, but it loads the data from the selected file into the text view.

You can customize the open/save panels further by setting other optional properties. This minimal solution implements a full open/save application with editing, copy/paste, and file save and load — all with a few lines of code. The finished application is shown in Figure 10.6.

![](bbox=[0.103, 0.8, 0.173, 0.856])

> **CAUTION**
> 
> If your Mac is on a network and you are connected to any remote servers, the open and save panes will scan the network and ping the servers. This isn't usually a problem, but if you are using a network monitor like Little Snitch, don't be surprised when your minimal application triggers a network access warning.