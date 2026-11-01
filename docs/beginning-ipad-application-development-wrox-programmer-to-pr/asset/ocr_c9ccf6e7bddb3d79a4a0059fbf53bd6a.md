7. Run the application a second time and it prints the content of the .plist file in the Documents directory to the Debugger Console window (see Figure 9-6), proving the existence of the property list in the Documents folder.

![](bbox=[0.18, 0.22, 0.78, 0.6])

FIGURE 9-6

# How It Works

The first part of this example shows how you can add a property list file to your application. In the property list file, you add three keys representing the category of applications in the AppStore: Entertainment, Games, and Utilities. Each category contains a list of application titles.

When the view is loaded, you look for a file named Apps.plist in the Documents directory of your application:

```
```objc
//---get the path to the property list file---
NSString *plistFileName =
    [[self documentsPath] stringByAppendingPathComponent:@"Apps.plist"];
```
```

If the file is found, you load its content into an NSDictionary object:

```
```objc
//---if the property list file can be found---
if ([[NSFileManager defaultManager] fileExistsAtPath:plistFileName]) {
    //---load the content of the property list file into a NSDictionary
    // object---
    NSDictionary *dict = [[NSDictionary alloc]
                          initWithContentsOfFile:plistFileName];
    //...
    //...
}
```
```

Next, you enumerate through all the keys in the dictionary object and print the title of each application in the Debugger Console window:

```
```objc
//---for each category---
for (NSString *category in dict) {
    NSLog(category);
```
```